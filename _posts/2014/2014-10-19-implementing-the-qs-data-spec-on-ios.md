---
layout: post
title: 'Implementing the QS Data Spec on iOS'
tags:
- drafts
- dropbox
- launchcenterpro
- quantifiedself
---

As part of implementing the [Quantified Self Data Spec][1] ([look here for an introduction][2]), I've started implementing it on iOS so that I'm living with it every day. The implementation I'm about to outline leverages the following technologies:

*   [The QS Data Spec][1], of course
*   [Dropbox][3]
*   [Launch Center Pro][4]
*   [Drafts 4][5]

![Workflow Overview][6]

## Launch Center Pro

Launch Center Pro is the perfect dashboard for testing (and even long-term running) of custom QS data collection efforts. You can set up multiple 1-touch actions to rapidly log many data points and have it integrate with other apps on your iOS device via URL-schemes if necessary. Notably, this process I'm using passes off to Drafts 4.

While it is possible to save files directly to Dropbox from Launch Center Pro, in order to fully support/implement the QS Data Spec I needed to be able to have a little more dynamic control over the JSON data before it was saved. You will see that my Launch Center Pro actions are missing the required `uuid` and `timestamp` JSON parameters. These will be inserted with Drafts later in the process.

I am going to demonstrate two basic workflow types: single-step (one touch) and multi-step. I've set up a emotional logger as the multi-step example, and a bathroom logger as the single-step example. For the bathroom logger, there are actually multiple single-step actions that I've grouped in to a folder, to make it more organized. I'm using single-step actions for this since it happens multiple times a day and I wanted to ensure it was as efficient as possible.

![Launch Center Pro][7]

### Single-step Action (Bathroom log)

This one is very simple. We need to pass a URL-encoded version of the base JSON object for this datatype to Drafts for further processing. Here's what the QS Data Spec says the [JSON object should look like][8] ([full schema][9]):

    {
      "dataType": "consumption-waste",
      "dataSource": "manual",
      "uuid": "2b0b8801-c5e2-4b2d-a61a-31681eb95093",
      "timestamp": 1413555528,
      "urine": true,
      "feces": false
    }
    

*(Note: while the spec is very medical, I labeled things a little more politely in Launch Center Pro. i.e. feces -> BM)*

As I mentioned previously, we will add the uuid and timestamp values dynamically within Drafts, so our Launch Center Pro action simply looks like this:

    drafts4://x-callback-url/runAction?text={{%7B%22dataType%22%3A%22consumption-waste%22%2C%22dataSource%22%3A%22manual%22%2C%22urine%22%3Atrue%2C%22feces%22%3Afalse%7D}}&action={{Log QuantifiedSelf Entry}}&x-success={{launch:}}
    

This action is basically saying do the following steps:

1.  Launch Drafts 4
2.  Get ready to run an action
3.  Pass in the URL encoded text for the JSON object
4.  Run the 'Log QuantifiedSelf Entry' action
5.  On success, come back to Launch Center Pro

### Multi-step Action (Emotional log)

![Launch Center Pro - Emotional][10]

The multi-step example follows the identical process as the single-step example except that it prompts the user for a few inputs before sending the JSON object over to Drafts. Here is what the QS Data Spec says the [emotional object should look like][11] ([full schema][12]):

    {
      "dataType":"biometric-emotional",
      "dataSource":"manual",
      "energyLevel":5,
      "mood":3,
      "stressLevel":1,
      "uuid":"64759c11-e432-45a9-ad1b-a49b791549e9",
      "timestamp":1413765928
    }
    

Our Launch Center Pro action, complete with user prompts to select the values of the three inputs looks like this:

    drafts4://x-callback-url/runAction?text={{%7B%22dataType%22%3A%22biometric-emotional%22%2C%22dataSource%22%3A%22manual%22%2C%22energyLevel%22%3A[list:Energy Level|Energetic=5|Alert=4|Neutral=3|Tired=2|Exhausted=1]%2C%22mood%22%3A[list:Mood|Amazing=5|Good=4|Okay=3|Bad=2|Terrible=1]%2C%22stressLevel%22%3A[list:Stress Level|Stressed=5|Anxious=4|Neutral=3|Relaxed=2|Chill=1]%7D}}&action={{Log QuantifiedSelf Entry}}&x-success={{launch:}}
    

### Bonus! Medical Log

You get the picture, right? So as a bonus we have the [QS Data Spec example for medicine][13] ([full schema][14]):

    {
      "dataType": "consumption-drug",
      "dataSource": "manual",
      "uuid": "2b0b8801-c5e2-4b2d-a61a-31681eb95093",
      "timestamp": 1413555528,
      "drug": "Ibuprofen",
      "amount": 200,
      "measurementScale": "mg"
    }
    

And the corresponding Launch Center Pro action, customized with entries for Ibuprofen and Ranitidine:

    drafts4://x-callback-url/runAction?text={{%7B%22dataType%22%3A%22consumption-waste%22%2C%22dataSource%22%3A%22manual%22%2C%22urine%22%3Atrue%2C%22feces%22%3Afalse%7D}}&action={{Log QuantifiedSelf Entry}}&x-success={{launch:}}
    

## Drafts 4

![Drafts Action Overview][15]

The quickest way to get this custom action into Drafts is from the Drafts Action Directory. I've [posted it here][16].

The Drafts action is pretty straightforward. To contain a JavaScript file and a save to Dropbox action. To keep the files more organized until I can process them at a later date, I've told drafts to save the files in a date-based file system hierarchy: Logs/[year]/[month]/[day]/[UUID].json

The JavaScript is fairly simple itself. It basically sets the timestamp and UUID, and then saves the file to Dropbox with the UUID as the filename. It ends up looking more complicated because I had to paste in support-methods for UUID and JSON.

    // Create the JSON object
    var jsonString = decodeURIComponent(draft.content);
    var j = JSON.parse(jsonString)
    
    // Generate and set a UUID
    var uuid = makeUUID();
    j.uuid = uuid;
    
    // Set the timestamp
    j.timestamp = Math.round((new Date()).getTime() / 1000);
    
    // Prep the Draft for saving to Dropbox in the next action step
    draft.content = JSON.stringify(j);
    
    // Send the UUID to the clipboard, so the next action can use it as the filename.
    setClipboard(uuid);
    
    // UUID support
    function makeUUID(){
    
      var dec2hex = [];
      for (var i=0; i<=15; i++) {
        dec2hex[i] = i.toString(16);
      }
    
        var uuid = '';
        for (var i=1; i<=36; i++) {
          if (i===9 || i===14 || i===19 || i===24) {
            uuid += '-';
          } else if (i===15) {
            uuid += 4;
          } else if (i===20) {
            uuid += dec2hex[(Math.random()*4|0 + 8)];
          } else {
            uuid += dec2hex[(Math.random()*15|0)];
          }
        }
    
        return uuid;
    }
    
    // JSON support
    var JSON;if(!JSON){JSON={}}(function(){function f(n){return n<10?"0"+n:n}if(typeof Date.prototype.toJSON!=="function"){Date.prototype.toJSON=function(key){return isFinite(this.valueOf())?this.getUTCFullYear()+"-"+f(this.getUTCMonth()+1)+"-"+f(this.getUTCDate())+"T"+f(this.getUTCHours())+":"+f(this.getUTCMinutes())+":"+f(this.getUTCSeconds())+"Z":null};String.prototype.toJSON=Number.prototype.toJSON=Boolean.prototype.toJSON=function(key){return this.valueOf()}}var cx=/[\u0000\u00ad\u0600-\u0604\u070f\u17b4\u17b5\u200c-\u200f\u2028-\u202f\u2060-\u206f\ufeff\ufff0-\uffff]/g,escapable=/[\\"\x00-\x1f\x7f-\x9f\u00ad\u0600-\u0604\u070f\u17b4\u17b5\u200c-\u200f\u2028-\u202f\u2060-\u206f\ufeff\ufff0-\uffff]/g,gap,indent,meta={"\b":"\b","\t":"\t","\n":"\n","\f":"\f","\r":"\r",'"':'\"',"\":"\\"},rep;function quote(string){escapable.lastIndex=0;return escapable.test(string)?'"'+string.replace(escapable,function(a){var c=meta[a];return typeof c==="string"?c:"\u"+("0000"+a.charCodeAt(0).toString(16)).slice(-4)})+'"':'"'+string+'"'}function str(key,holder){var i,k,v,length,mind=gap,partial,value=holder[key];if(value&&typeof value==="object"&&typeof value.toJSON==="function"){value=value.toJSON(key)}if(typeof rep==="function"){value=rep.call(holder,key,value)}switch(typeof value){case"string":return quote(value);case"number":return isFinite(value)?String(value):"null";case"boolean":case"null":return String(value);case"object":if(!value){return"null"}gap+=indent;partial=[];if(Object.prototype.toString.apply(value)==="[object Array]"){length=value.length;for(i=0;i<length;i+=1){partial[i]=str(i,value)||"null"}v=partial.length===0?"[]":gap?"[\n"+gap+partial.join(",\n"+gap)+"\n"+mind+"]":"["+partial.join(",")+"]";gap=mind;return v}if(rep&&typeof rep==="object"){length=rep.length;for(i=0;i<length;i+=1){if(typeof rep[i]==="string"){k=rep[i];v=str(k,value);if(v){partial.push(quote(k)+(gap?": ":":")+v)}}}}else{for(k in value){if(Object.prototype.hasOwnProperty.call(value,k)){v=str(k,value);if(v){partial.push(quote(k)+(gap?": ":":")+v)}}}}v=partial.length===0?"{}":gap?"{\n"+gap+partial.join(",\n"+gap)+"\n"+mind+"}":"{"+partial.join(",")+"}";gap=mind;return v}}if(typeof JSON.stringify!=="function"){JSON.stringify=function(value,replacer,space){var i;gap="";indent="";if(typeof space==="number"){for(i=0;i<space;i+=1){indent+=" "}}else{if(typeof space==="string"){indent=space}}rep=replacer;if(replacer&&typeof replacer!=="function"&&(typeof replacer!=="object"||typeof replacer.length!=="number")){throw new Error("JSON.stringify")}return str("",{"":value})}}if(typeof JSON.parse!=="function"){JSON.parse=function(text,reviver){var j;function walk(holder,key){var k,v,value=holder[key];if(value&&typeof value==="object"){for(k in value){if(Object.prototype.hasOwnProperty.call(value,k)){v=walk(value,k);if(v!==undefined){value[k]=v}else{delete value[k]}}}}return reviver.call(holder,key,value)}text=String(text);cx.lastIndex=0;if(cx.test(text)){text=text.replace(cx,function(a){return"\u"+("0000"+a.charCodeAt(0).toString(16)).slice(-4)})}if(/^[],:{}\s]*$/.test(text.replace(/\(?:["\\/bfnrt]|u[0-9a-fA-F]{4})/g,"@").replace(/"[^"\\n\r]*"|true|false|null|-?\d+(?:.\d*)?(?:[eE][+-]?\d+)?/g,"]").replace(/(?:^|:|,)(?:\s*[)+/g,""))){j=eval("("+text+")");return typeof reviver==="function"?walk({"":j},""):j}throw new SyntaxError("JSON.parse")}}}());

 [1]: https://github.com/nateswart/QuantifiedSelf-Data-Spec
 [2]: /2014/10/18/the-beginning-of-a-qs-data-spec
 [3]: https://db.tt/Ky7oLc1
 [4]: http://contrast.co/launch-center-pro/
 [5]: http://agiletortoise.com/drafts/
 [6]: /public/post-images/2014/iOSQSOverview.png
 [7]: /public/post-images/2014/lcp.png
 [8]: https://github.com/nateswart/QuantifiedSelf-Data-Spec/blob/master/Consumption/examples/consumption-waste.json
 [9]: https://github.com/nateswart/QuantifiedSelf-Data-Spec/blob/master/Consumption/consumption-waste.json
 [10]: /public/post-images/2014/lcp_emotional.png
 [11]: https://github.com/nateswart/QuantifiedSelf-Data-Spec/blob/master/Biometric/examples/biometric-emotional.json
 [12]: https://github.com/nateswart/QuantifiedSelf-Data-Spec/blob/master/Biometric/biometric-emotional.json
 [13]: https://github.com/nateswart/QuantifiedSelf-Data-Spec/blob/master/Consumption/examples/consumption-drug.json
 [14]: https://github.com/nateswart/QuantifiedSelf-Data-Spec/blob/master/Consumption/consumption-drug.json
 [15]: /public/post-images/2014/Drafts-Action.png
 [16]: http://drafts4-actions.agiletortoise.com/a/1HD