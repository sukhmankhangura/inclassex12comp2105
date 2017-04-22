// global javascript used on even the oldest themes

var RecaptchaOptions = {theme : 'clean'};

var ns4  = document.layers;
var dom5 = document.getElementById;
var ie4  = document.all && !dom5;

// One object tracks the current modal dialog opened from this window.
var dialogWin = new Object();

// Generate a modal dialog.
// Parameters:
//    url :			URL of the page/frameset to be loaded into dialog
//    width :		pixel width of the dialog window
//    height :		pixel height of the dialog window
//    returnFunc :	reference to the function (on this page)
//                  that is to act on the data returned from the dialog
//    args : [optional] any data you need to pass to the dialog
//FIXME: not used?
function openDialogWithReferrer(url, width, height) {
	var name = (new Date()).valueOf();
	var urlpath = new String(window.location.href);
	urlpath = urlpath.substr(0,urlpath.lastIndexOf('/')+1);
	urlpath = escape(urlpath);
	url = url + "&qsReferrer=" + urlpath;
	openNamedDialog(url, width, height, name, false);
}
//FIXME: not used?
function openTargetDialog(url, width, height, theform) {
	var windowName = (new Date()).valueOf();
	theform.target = windowName;
	openNamedDialog(url, width, height, windowName);
}
function openDialog(url, width, height) {
	var name = (new Date()).valueOf();
	openNamedDialog(url, width, height, name, false);
}
//FIXME: only called from this file
function openNamedDialog(url, width, height, name, bStatusBar) {
	if (!dialogWin.win || (dialogWin.win && dialogWin.win.closed)) {
		// Initialize properties of the modal dialog object.
		if (url.indexOf('?') >=0 ) {
			url += '&dialog=1';
		} else {
			url += '?dialog=1';
		}
		dialogWin.url = url;
		dialogWin.width = width;
		dialogWin.height = height;
		dialogWin.name = name;
		// Assemble window attributes and try to center the dialog.
		if (ns4) {
			// Center on the main window.
			dialogWin.left = window.screenX + ((window.outerWidth - dialogWin.width) / 2);
			dialogWin.top = window.screenY + ((window.outerHeight - dialogWin.height) / 2);
			var attr = "screenX=" + dialogWin.left + 
				 ",screenY=" + dialogWin.top + 
				 ",resizable=yes,width=" + dialogWin.width + 
				 ",height=" + dialogWin.height +
				 ",scrollbars=yes";
			if (bStatusBar) attr = attr + 
				",status=yes,toolbar=no,location=no" +
				",personalbar=no,menubar=no,directories=no";
		} else {
			// The best we can do is center in screen.
			dialogWin.left = (screen.width - dialogWin.width) / 2;
			dialogWin.top = (screen.height - dialogWin.height) / 2;
			var sStatusBar
			sStatusBar = bStatusBar ? "yes" : "no";
			var attr = "width=" + dialogWin.width + 
				",height=" + dialogWin.height + 
				",menubar=no" + 
				",scrollbars=yes" + 
				",toolbar=no" + 
				",location=no" + 
				",directories=no" + 
				",resizable=yes" + 
				",personalbar=no" + 
				",status="  + sStatusBar +
				",top=" + dialogWin.top + 
				",left=" + dialogWin.left;
		}
		// Generate the dialog and make sure it has focus.
		dialogWin.win=window.open(dialogWin.url, dialogWin.name, attr);
		dialogWin.win.focus();
	} else {
		dialogWin.win.focus();
	}
}

// Because browsers can be a bit slow at closing windows,
// we must wait 250ms before checking if the modal window is still open.
var timeoutID = false;
// FIXME: not used
function checkModal() {
	if (timeoutID != false) window.clearTimeout(timeoutID);
	timeoutID = window.setTimeout("finishChecking()", 250);
}
// FIXME: not used
function finishChecking() {
	timeoutID = false;
	if (dialogWin.win) {
		if (!dialogWin.win.closed) {
			dialogWin.win.focus();
		}
	}
}

// When actually using the fake Modal Dialog Box, link as follows:
// (&gt;) A HREF="#" onClick="openDialog('popup_edit.php', 400, 300); 
// return false;" (&lt;) Preferences (&gt;) /a (&lt;)

function isitEmail(str) {
	var r1 = new RegExp("(@.*@)|(\\.\\.)|(@\\.)|(^\\.)");
	var r2 = new RegExp("^.+\\@(\\[?)[a-zA-Z0-9\\-\\.]+\\.([a-zA-Z]{2,6}|[0-9]{1,3})(\\]?)$");
	return (!r1.test(str) && r2.test(str));
}

function getObject(objectId) {
		// cross-browser function to get an object's style object given its id
		if(document.getElementById && document.getElementById(objectId)) {
		// W3C DOM
		return document.getElementById(objectId);
		} else if (document.all && document.all(objectId)) {
		// MSIE 4 DOM
		return document.all(objectId);
		} else if (document.layers && document.layers[objectId]) {
		// NN 4 DOM.. note: this won't find nested layers
		return document.layers[objectId];
		} else {
		return false;
		}
} // getObject


function previewTheme(themeID) {
	var preview = getObject("imgTheme");
	var thumbnail = getObject("imgTheme_"+themeID);
	preview.src =thumbnail.src;
}
function rollOverTheme(themeID) {
	previewTheme(themeID);
}
function rollOutTheme(themeID) {
	previewTheme(iThemeID); //return to the default
}
function clickedTheme(themeID) {
	var input = getObject("fiThemeID_"+themeID);
	if (input && !input.checked) {
		input.checked = true;
	}
	previewTheme(themeID);
	iThemeID = themeID;
}
function previewLayout(layoutID) {
	var preview = getObject("imgLayout");
	var thumbnail = getObject("imgLayout_"+layoutID);
	if (preview && thumbnail) preview.src = thumbnail.src;
}
function rollOverLayout(layoutID) {
	previewLayout(layoutID);
}
function rollOutLayout(leavingLayoutID) {
	previewLayout(iLayoutID); //return to the globally selected layout
}
function clickedLayout(layoutID) {
	previewLayout(layoutID);
	var input = getObject("fiLayout_"+layoutID);
	if (input && !input.checked) {
		input.checked = true;
	}
	iLayoutID = layoutID;
}

function showLayer(id) {
	document.getElementById(id).style.visibility = 'visible';
}
function hideLayer(id) {
	document.getElementById(id).style.visibility = 'hidden';
}

function changeToolbar(id) {
	var w = window;
	while (w && w != w.parent && !w.frames['menuframe'])
		w = w.parent;
	w.frames['menuframe'].setCBox(id);
}

function openGuidedTourWin(iTier) {
	var attr = "resizable=no,width=600,height=400,scrollbars=yes";
	var url = (iTier==1) ? 'templates/guidedtour_budget1.htm' : 'templates/guidedtour_guildnet1.htm';
	var windowName = (new Date()).valueOf();
	// Generate the dialog and make sure it has focus.
	var win;
	win=window.open(url, windowName, attr);
	win.focus();
}

function filePopup(url) {
		var d = new Date();
		var wn = "ag" + d.valueOf();
		window.open(url,wn,"toolbar=no, directories=no, location=no, status=yes, menubar=no, scrollbars=yes, width=750, height=550");
		return false;
}

function closePopupForm() {
	try {
		if (window.opener) {
			if (window.opener.top && window.opener.top.frames["menuframe"]) {
				window.opener.top.frames["menuframe"].bDataChanged = true;
			}
			window.opener.location.reload();
		} 
	} catch (e) {}
	window.close();
}

