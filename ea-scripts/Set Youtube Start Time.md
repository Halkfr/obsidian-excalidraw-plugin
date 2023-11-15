/* 

This script allows you to set the starting time of a YouTube video or shorts by editing the link of the chosen YouTube video on your canvas. Script adds "?t=" followed by the specified time from the modal window to the edited link.

```javascript
*/
const selectedElement = ea.getViewSelectedElement();

if (!selectedElement) {
	new Notice("Please select youtube video");
	return;
}
const link = selectedElement.link;
const regex = /^(?:http(?:s)?:\/\/)?(?:(?:w){3}.)?youtu(?:be|.be)?(?:\.com)?\/(?:embed\/|watch\?v=|shorts\/)?([a-zA-Z0-9_-]+)/;

let time = await utils.inputPrompt("Set start time", "ss, mm:ss, hh:mm:ss");

if (time) {
	const timeArr = time.split(':');
	let seconds = 0;
	for (let i = 0; i < timeArr.length; i++) {
		seconds += Number(timeArr[i]) * Math.pow(60, timeArr.length - 1 - i);
	}
	selectedElement.link = regex.exec(link)[0] + "?t=" + seconds;
}
