---
title: "Graph Measure Implementations"
excerpt: "A collection of graph measures to compute on numpy arrays."
header:
  teaser: "assets/images/posts/graph_measures_implementation.png"
  overlay_image: "assets/images/posts/graph_measures_implementation.png"
  overlay_text: ""
tags:
  - Complex Systems
  - Data Analysis
---

Making Sense of networks can be hard. In some cases, using graph theory can help to understand certain properties of the underlying network, even though the network itself is too complex to understand.
In the following script, you can investigate Python implementations for a number of graph theory measures which we used to analyze brain connectivity patterns.

<!DOCTYPE html>
<html>
<head><meta charset="utf-8" />

<title>graph_measures_implementation</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>



<style type="text/css">
    /*!
*
* Twitter Bootstrap
*
*/
/*!
 * Bootstrap v3.3.7 (http://getbootstrap.com)
 * Copyright 2011-2016 Twitter, Inc.
 * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
 */
/*! normalize.css v3.0.3 | MIT License | github.com/necolas/normalize.css */
html {
  font-family: sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}
body {
  margin: 0;
}
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
menu,
nav,
section,
summary {
  display: block;
}
audio,
canvas,
progress,
video {
  display: inline-block;
  vertical-align: baseline;
}
audio:not([controls]) {
  display: none;
  height: 0;
}
[hidden],
template {
  display: none;
}
a {
  background-color: transparent;
}
a:active,
a:hover {
  outline: 0;
}
abbr[title] {
  border-bottom: 1px dotted;
}
b,
strong {
  font-weight: bold;
}
dfn {
  font-style: italic;
}
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}
mark {
  background: #ff0;
  color: #000;
}
small {
  font-size: 80%;
}
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}
sup {
  top: -0.5em;
}
sub {
  bottom: -0.25em;
}
img {
  border: 0;
}
svg:not(:root) {
  overflow: hidden;
}
figure {
  margin: 1em 40px;
}
hr {
  box-sizing: content-box;
  height: 0;
}
pre {
  overflow: auto;
}
code,
kbd,
pre,
samp {
  font-family: monospace, monospace;
  font-size: 1em;
}
button,
input,
optgroup,
select,
textarea {
  color: inherit;
  font: inherit;
  margin: 0;
}
button {
  overflow: visible;
}
button,
select {
  text-transform: none;
}
button,
html input[type="button"],
input[type="reset"],
input[type="submit"] {
  -webkit-appearance: button;
  cursor: pointer;
}
button[disabled],
html input[disabled] {
  cursor: default;
}
button::-moz-focus-inner,
input::-moz-focus-inner {
  border: 0;
  padding: 0;
}
input {
  line-height: normal;
}
input[type="checkbox"],
input[type="radio"] {
  box-sizing: border-box;
  padding: 0;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: textfield;
  box-sizing: content-box;
}
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}
fieldset {
  border: 1px solid #c0c0c0;
  margin: 0 2px;
  padding: 0.35em 0.625em 0.75em;
}
legend {
  border: 0;
  padding: 0;
}
textarea {
  overflow: auto;
}
optgroup {
  font-weight: bold;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
td,
th {
  padding: 0;
}
/*! Source: https://github.com/h5bp/html5-boilerplate/blob/master/src/css/main.css */
@media print {
  *,
  *:before,
  *:after {
    background: transparent !important;
    box-shadow: none !important;
    text-shadow: none !important;
  }
  a,
  a:visited {
    text-decoration: underline;
  }
  a[href]:after {
    content: " (" attr(href) ")";
  }
  abbr[title]:after {
    content: " (" attr(title) ")";
  }
  a[href^="#"]:after,
  a[href^="javascript:"]:after {
    content: "";
  }
  pre,
  blockquote {
    border: 1px solid #999;
    page-break-inside: avoid;
  }
  thead {
    display: table-header-group;
  }
  tr,
  img {
    page-break-inside: avoid;
  }
  img {
    max-width: 100% !important;
  }
  p,
  h2,
  h3 {
    orphans: 3;
    widows: 3;
  }
  h2,
  h3 {
    page-break-after: avoid;
  }
  .navbar {
    display: none;
  }
  .btn > .caret,
  .dropup > .btn > .caret {
    border-top-color: #000 !important;
  }
  .label {
    border: 1px solid #000;
  }
  .table {
    border-collapse: collapse !important;
  }
  .table td,
  .table th {
    background-color: #fff !important;
  }
  .table-bordered th,
  .table-bordered td {
    border: 1px solid #ddd !important;
  }
}
@font-face {
  font-family: 'Glyphicons Halflings';
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot');
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot?#iefix') format('embedded-opentype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff2') format('woff2'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff') format('woff'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.ttf') format('truetype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.svg#glyphicons_halflingsregular') format('svg');
}
.glyphicon {
  position: relative;
  top: 1px;
  display: inline-block;
  font-family: 'Glyphicons Halflings';
  font-style: normal;
  font-weight: normal;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.glyphicon-asterisk:before {
  content: "\002a";
}
.glyphicon-plus:before {
  content: "\002b";
}
.glyphicon-euro:before,
.glyphicon-eur:before {
  content: "\20ac";
}
.glyphicon-minus:before {
  content: "\2212";
}
.glyphicon-cloud:before {
  content: "\2601";
}
.glyphicon-envelope:before {
  content: "\2709";
}
.glyphicon-pencil:before {
  content: "\270f";
}
.glyphicon-glass:before {
  content: "\e001";
}
.glyphicon-music:before {
  content: "\e002";
}
.glyphicon-search:before {
  content: "\e003";
}
.glyphicon-heart:before {
  content: "\e005";
}
.glyphicon-star:before {
  content: "\e006";
}
.glyphicon-star-empty:before {
  content: "\e007";
}
.glyphicon-user:before {
  content: "\e008";
}
.glyphicon-film:before {
  content: "\e009";
}
.glyphicon-th-large:before {
  content: "\e010";
}
.glyphicon-th:before {
  content: "\e011";
}
.glyphicon-th-list:before {
  content: "\e012";
}
.glyphicon-ok:before {
  content: "\e013";
}
.glyphicon-remove:before {
  content: "\e014";
}
.glyphicon-zoom-in:before {
  content: "\e015";
}
.glyphicon-zoom-out:before {
  content: "\e016";
}
.glyphicon-off:before {
  content: "\e017";
}
.glyphicon-signal:before {
  content: "\e018";
}
.glyphicon-cog:before {
  content: "\e019";
}
.glyphicon-trash:before {
  content: "\e020";
}
.glyphicon-home:before {
  content: "\e021";
}
.glyphicon-file:before {
  content: "\e022";
}
.glyphicon-time:before {
  content: "\e023";
}
.glyphicon-road:before {
  content: "\e024";
}
.glyphicon-download-alt:before {
  content: "\e025";
}
.glyphicon-download:before {
  content: "\e026";
}
.glyphicon-upload:before {
  content: "\e027";
}
.glyphicon-inbox:before {
  content: "\e028";
}
.glyphicon-play-circle:before {
  content: "\e029";
}
.glyphicon-repeat:before {
  content: "\e030";
}
.glyphicon-refresh:before {
  content: "\e031";
}
.glyphicon-list-alt:before {
  content: "\e032";
}
.glyphicon-lock:before {
  content: "\e033";
}
.glyphicon-flag:before {
  content: "\e034";
}
.glyphicon-headphones:before {
  content: "\e035";
}
.glyphicon-volume-off:before {
  content: "\e036";
}
.glyphicon-volume-down:before {
  content: "\e037";
}
.glyphicon-volume-up:before {
  content: "\e038";
}
.glyphicon-qrcode:before {
  content: "\e039";
}
.glyphicon-barcode:before {
  content: "\e040";
}
.glyphicon-tag:before {
  content: "\e041";
}
.glyphicon-tags:before {
  content: "\e042";
}
.glyphicon-book:before {
  content: "\e043";
}
.glyphicon-bookmark:before {
  content: "\e044";
}
.glyphicon-print:before {
  content: "\e045";
}
.glyphicon-camera:before {
  content: "\e046";
}
.glyphicon-font:before {
  content: "\e047";
}
.glyphicon-bold:before {
  content: "\e048";
}
.glyphicon-italic:before {
  content: "\e049";
}
.glyphicon-text-height:before {
  content: "\e050";
}
.glyphicon-text-width:before {
  content: "\e051";
}
.glyphicon-align-left:before {
  content: "\e052";
}
.glyphicon-align-center:before {
  content: "\e053";
}
.glyphicon-align-right:before {
  content: "\e054";
}
.glyphicon-align-justify:before {
  content: "\e055";
}
.glyphicon-list:before {
  content: "\e056";
}
.glyphicon-indent-left:before {
  content: "\e057";
}
.glyphicon-indent-right:before {
  content: "\e058";
}
.glyphicon-facetime-video:before {
  content: "\e059";
}
.glyphicon-picture:before {
  content: "\e060";
}
.glyphicon-map-marker:before {
  content: "\e062";
}
.glyphicon-adjust:before {
  content: "\e063";
}
.glyphicon-tint:before {
  content: "\e064";
}
.glyphicon-edit:before {
  content: "\e065";
}
.glyphicon-share:before {
  content: "\e066";
}
.glyphicon-check:before {
  content: "\e067";
}
.glyphicon-move:before {
  content: "\e068";
}
.glyphicon-step-backward:before {
  content: "\e069";
}
.glyphicon-fast-backward:before {
  content: "\e070";
}
.glyphicon-backward:before {
  content: "\e071";
}
.glyphicon-play:before {
  content: "\e072";
}
.glyphicon-pause:before {
  content: "\e073";
}
.glyphicon-stop:before {
  content: "\e074";
}
.glyphicon-forward:before {
  content: "\e075";
}
.glyphicon-fast-forward:before {
  content: "\e076";
}
.glyphicon-step-forward:before {
  content: "\e077";
}
.glyphicon-eject:before {
  content: "\e078";
}
.glyphicon-chevron-left:before {
  content: "\e079";
}
.glyphicon-chevron-right:before {
  content: "\e080";
}
.glyphicon-plus-sign:before {
  content: "\e081";
}
.glyphicon-minus-sign:before {
  content: "\e082";
}
.glyphicon-remove-sign:before {
  content: "\e083";
}
.glyphicon-ok-sign:before {
  content: "\e084";
}
.glyphicon-question-sign:before {
  content: "\e085";
}
.glyphicon-info-sign:before {
  content: "\e086";
}
.glyphicon-screenshot:before {
  content: "\e087";
}
.glyphicon-remove-circle:before {
  content: "\e088";
}
.glyphicon-ok-circle:before {
  content: "\e089";
}
.glyphicon-ban-circle:before {
  content: "\e090";
}
.glyphicon-arrow-left:before {
  content: "\e091";
}
.glyphicon-arrow-right:before {
  content: "\e092";
}
.glyphicon-arrow-up:before {
  content: "\e093";
}
.glyphicon-arrow-down:before {
  content: "\e094";
}
.glyphicon-share-alt:before {
  content: "\e095";
}
.glyphicon-resize-full:before {
  content: "\e096";
}
.glyphicon-resize-small:before {
  content: "\e097";
}
.glyphicon-exclamation-sign:before {
  content: "\e101";
}
.glyphicon-gift:before {
  content: "\e102";
}
.glyphicon-leaf:before {
  content: "\e103";
}
.glyphicon-fire:before {
  content: "\e104";
}
.glyphicon-eye-open:before {
  content: "\e105";
}
.glyphicon-eye-close:before {
  content: "\e106";
}
.glyphicon-warning-sign:before {
  content: "\e107";
}
.glyphicon-plane:before {
  content: "\e108";
}
.glyphicon-calendar:before {
  content: "\e109";
}
.glyphicon-random:before {
  content: "\e110";
}
.glyphicon-comment:before {
  content: "\e111";
}
.glyphicon-magnet:before {
  content: "\e112";
}
.glyphicon-chevron-up:before {
  content: "\e113";
}
.glyphicon-chevron-down:before {
  content: "\e114";
}
.glyphicon-retweet:before {
  content: "\e115";
}
.glyphicon-shopping-cart:before {
  content: "\e116";
}
.glyphicon-folder-close:before {
  content: "\e117";
}
.glyphicon-folder-open:before {
  content: "\e118";
}
.glyphicon-resize-vertical:before {
  content: "\e119";
}
.glyphicon-resize-horizontal:before {
  content: "\e120";
}
.glyphicon-hdd:before {
  content: "\e121";
}
.glyphicon-bullhorn:before {
  content: "\e122";
}
.glyphicon-bell:before {
  content: "\e123";
}
.glyphicon-certificate:before {
  content: "\e124";
}
.glyphicon-thumbs-up:before {
  content: "\e125";
}
.glyphicon-thumbs-down:before {
  content: "\e126";
}
.glyphicon-hand-right:before {
  content: "\e127";
}
.glyphicon-hand-left:before {
  content: "\e128";
}
.glyphicon-hand-up:before {
  content: "\e129";
}
.glyphicon-hand-down:before {
  content: "\e130";
}
.glyphicon-circle-arrow-right:before {
  content: "\e131";
}
.glyphicon-circle-arrow-left:before {
  content: "\e132";
}
.glyphicon-circle-arrow-up:before {
  content: "\e133";
}
.glyphicon-circle-arrow-down:before {
  content: "\e134";
}
.glyphicon-globe:before {
  content: "\e135";
}
.glyphicon-wrench:before {
  content: "\e136";
}
.glyphicon-tasks:before {
  content: "\e137";
}
.glyphicon-filter:before {
  content: "\e138";
}
.glyphicon-briefcase:before {
  content: "\e139";
}
.glyphicon-fullscreen:before {
  content: "\e140";
}
.glyphicon-dashboard:before {
  content: "\e141";
}
.glyphicon-paperclip:before {
  content: "\e142";
}
.glyphicon-heart-empty:before {
  content: "\e143";
}
.glyphicon-link:before {
  content: "\e144";
}
.glyphicon-phone:before {
  content: "\e145";
}
.glyphicon-pushpin:before {
  content: "\e146";
}
.glyphicon-usd:before {
  content: "\e148";
}
.glyphicon-gbp:before {
  content: "\e149";
}
.glyphicon-sort:before {
  content: "\e150";
}
.glyphicon-sort-by-alphabet:before {
  content: "\e151";
}
.glyphicon-sort-by-alphabet-alt:before {
  content: "\e152";
}
.glyphicon-sort-by-order:before {
  content: "\e153";
}
.glyphicon-sort-by-order-alt:before {
  content: "\e154";
}
.glyphicon-sort-by-attributes:before {
  content: "\e155";
}
.glyphicon-sort-by-attributes-alt:before {
  content: "\e156";
}
.glyphicon-unchecked:before {
  content: "\e157";
}
.glyphicon-expand:before {
  content: "\e158";
}
.glyphicon-collapse-down:before {
  content: "\e159";
}
.glyphicon-collapse-up:before {
  content: "\e160";
}
.glyphicon-log-in:before {
  content: "\e161";
}
.glyphicon-flash:before {
  content: "\e162";
}
.glyphicon-log-out:before {
  content: "\e163";
}
.glyphicon-new-window:before {
  content: "\e164";
}
.glyphicon-record:before {
  content: "\e165";
}
.glyphicon-save:before {
  content: "\e166";
}
.glyphicon-open:before {
  content: "\e167";
}
.glyphicon-saved:before {
  content: "\e168";
}
.glyphicon-import:before {
  content: "\e169";
}
.glyphicon-export:before {
  content: "\e170";
}
.glyphicon-send:before {
  content: "\e171";
}
.glyphicon-floppy-disk:before {
  content: "\e172";
}
.glyphicon-floppy-saved:before {
  content: "\e173";
}
.glyphicon-floppy-remove:before {
  content: "\e174";
}
.glyphicon-floppy-save:before {
  content: "\e175";
}
.glyphicon-floppy-open:before {
  content: "\e176";
}
.glyphicon-credit-card:before {
  content: "\e177";
}
.glyphicon-transfer:before {
  content: "\e178";
}
.glyphicon-cutlery:before {
  content: "\e179";
}
.glyphicon-header:before {
  content: "\e180";
}
.glyphicon-compressed:before {
  content: "\e181";
}
.glyphicon-earphone:before {
  content: "\e182";
}
.glyphicon-phone-alt:before {
  content: "\e183";
}
.glyphicon-tower:before {
  content: "\e184";
}
.glyphicon-stats:before {
  content: "\e185";
}
.glyphicon-sd-video:before {
  content: "\e186";
}
.glyphicon-hd-video:before {
  content: "\e187";
}
.glyphicon-subtitles:before {
  content: "\e188";
}
.glyphicon-sound-stereo:before {
  content: "\e189";
}
.glyphicon-sound-dolby:before {
  content: "\e190";
}
.glyphicon-sound-5-1:before {
  content: "\e191";
}
.glyphicon-sound-6-1:before {
  content: "\e192";
}
.glyphicon-sound-7-1:before {
  content: "\e193";
}
.glyphicon-copyright-mark:before {
  content: "\e194";
}
.glyphicon-registration-mark:before {
  content: "\e195";
}
.glyphicon-cloud-download:before {
  content: "\e197";
}
.glyphicon-cloud-upload:before {
  content: "\e198";
}
.glyphicon-tree-conifer:before {
  content: "\e199";
}
.glyphicon-tree-deciduous:before {
  content: "\e200";
}
.glyphicon-cd:before {
  content: "\e201";
}
.glyphicon-save-file:before {
  content: "\e202";
}
.glyphicon-open-file:before {
  content: "\e203";
}
.glyphicon-level-up:before {
  content: "\e204";
}
.glyphicon-copy:before {
  content: "\e205";
}
.glyphicon-paste:before {
  content: "\e206";
}
.glyphicon-alert:before {
  content: "\e209";
}
.glyphicon-equalizer:before {
  content: "\e210";
}
.glyphicon-king:before {
  content: "\e211";
}
.glyphicon-queen:before {
  content: "\e212";
}
.glyphicon-pawn:before {
  content: "\e213";
}
.glyphicon-bishop:before {
  content: "\e214";
}
.glyphicon-knight:before {
  content: "\e215";
}
.glyphicon-baby-formula:before {
  content: "\e216";
}
.glyphicon-tent:before {
  content: "\26fa";
}
.glyphicon-blackboard:before {
  content: "\e218";
}
.glyphicon-bed:before {
  content: "\e219";
}
.glyphicon-apple:before {
  content: "\f8ff";
}
.glyphicon-erase:before {
  content: "\e221";
}
.glyphicon-hourglass:before {
  content: "\231b";
}
.glyphicon-lamp:before {
  content: "\e223";
}
.glyphicon-duplicate:before {
  content: "\e224";
}
.glyphicon-piggy-bank:before {
  content: "\e225";
}
.glyphicon-scissors:before {
  content: "\e226";
}
.glyphicon-bitcoin:before {
  content: "\e227";
}
.glyphicon-btc:before {
  content: "\e227";
}
.glyphicon-xbt:before {
  content: "\e227";
}
.glyphicon-yen:before {
  content: "\00a5";
}
.glyphicon-jpy:before {
  content: "\00a5";
}
.glyphicon-ruble:before {
  content: "\20bd";
}
.glyphicon-rub:before {
  content: "\20bd";
}
.glyphicon-scale:before {
  content: "\e230";
}
.glyphicon-ice-lolly:before {
  content: "\e231";
}
.glyphicon-ice-lolly-tasted:before {
  content: "\e232";
}
.glyphicon-education:before {
  content: "\e233";
}
.glyphicon-option-horizontal:before {
  content: "\e234";
}
.glyphicon-option-vertical:before {
  content: "\e235";
}
.glyphicon-menu-hamburger:before {
  content: "\e236";
}
.glyphicon-modal-window:before {
  content: "\e237";
}
.glyphicon-oil:before {
  content: "\e238";
}
.glyphicon-grain:before {
  content: "\e239";
}
.glyphicon-sunglasses:before {
  content: "\e240";
}
.glyphicon-text-size:before {
  content: "\e241";
}
.glyphicon-text-color:before {
  content: "\e242";
}
.glyphicon-text-background:before {
  content: "\e243";
}
.glyphicon-object-align-top:before {
  content: "\e244";
}
.glyphicon-object-align-bottom:before {
  content: "\e245";
}
.glyphicon-object-align-horizontal:before {
  content: "\e246";
}
.glyphicon-object-align-left:before {
  content: "\e247";
}
.glyphicon-object-align-vertical:before {
  content: "\e248";
}
.glyphicon-object-align-right:before {
  content: "\e249";
}
.glyphicon-triangle-right:before {
  content: "\e250";
}
.glyphicon-triangle-left:before {
  content: "\e251";
}
.glyphicon-triangle-bottom:before {
  content: "\e252";
}
.glyphicon-triangle-top:before {
  content: "\e253";
}
.glyphicon-console:before {
  content: "\e254";
}
.glyphicon-superscript:before {
  content: "\e255";
}
.glyphicon-subscript:before {
  content: "\e256";
}
.glyphicon-menu-left:before {
  content: "\e257";
}
.glyphicon-menu-right:before {
  content: "\e258";
}
.glyphicon-menu-down:before {
  content: "\e259";
}
.glyphicon-menu-up:before {
  content: "\e260";
}
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
*:before,
*:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
html {
  font-size: 10px;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 13px;
  line-height: 1.42857143;
  color: #000;
  background-color: #fff;
}
input,
button,
select,
textarea {
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
a {
  color: #337ab7;
  text-decoration: none;
}
a:hover,
a:focus {
  color: #23527c;
  text-decoration: underline;
}
a:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
figure {
  margin: 0;
}
img {
  vertical-align: middle;
}
.img-responsive,
.thumbnail > img,
.thumbnail a > img,
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  display: block;
  max-width: 100%;
  height: auto;
}
.img-rounded {
  border-radius: 3px;
}
.img-thumbnail {
  padding: 4px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
  display: inline-block;
  max-width: 100%;
  height: auto;
}
.img-circle {
  border-radius: 50%;
}
hr {
  margin-top: 18px;
  margin-bottom: 18px;
  border: 0;
  border-top: 1px solid #eeeeee;
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
[role="button"] {
  cursor: pointer;
}
h1,
h2,
h3,
h4,
h5,
h6,
.h1,
.h2,
.h3,
.h4,
.h5,
.h6 {
  font-family: inherit;
  font-weight: 500;
  line-height: 1.1;
  color: inherit;
}
h1 small,
h2 small,
h3 small,
h4 small,
h5 small,
h6 small,
.h1 small,
.h2 small,
.h3 small,
.h4 small,
.h5 small,
.h6 small,
h1 .small,
h2 .small,
h3 .small,
h4 .small,
h5 .small,
h6 .small,
.h1 .small,
.h2 .small,
.h3 .small,
.h4 .small,
.h5 .small,
.h6 .small {
  font-weight: normal;
  line-height: 1;
  color: #777777;
}
h1,
.h1,
h2,
.h2,
h3,
.h3 {
  margin-top: 18px;
  margin-bottom: 9px;
}
h1 small,
.h1 small,
h2 small,
.h2 small,
h3 small,
.h3 small,
h1 .small,
.h1 .small,
h2 .small,
.h2 .small,
h3 .small,
.h3 .small {
  font-size: 65%;
}
h4,
.h4,
h5,
.h5,
h6,
.h6 {
  margin-top: 9px;
  margin-bottom: 9px;
}
h4 small,
.h4 small,
h5 small,
.h5 small,
h6 small,
.h6 small,
h4 .small,
.h4 .small,
h5 .small,
.h5 .small,
h6 .small,
.h6 .small {
  font-size: 75%;
}
h1,
.h1 {
  font-size: 33px;
}
h2,
.h2 {
  font-size: 27px;
}
h3,
.h3 {
  font-size: 23px;
}
h4,
.h4 {
  font-size: 17px;
}
h5,
.h5 {
  font-size: 13px;
}
h6,
.h6 {
  font-size: 12px;
}
p {
  margin: 0 0 9px;
}
.lead {
  margin-bottom: 18px;
  font-size: 14px;
  font-weight: 300;
  line-height: 1.4;
}
@media (min-width: 768px) {
  .lead {
    font-size: 19.5px;
  }
}
small,
.small {
  font-size: 92%;
}
mark,
.mark {
  background-color: #fcf8e3;
  padding: .2em;
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
.text-center {
  text-align: center;
}
.text-justify {
  text-align: justify;
}
.text-nowrap {
  white-space: nowrap;
}
.text-lowercase {
  text-transform: lowercase;
}
.text-uppercase {
  text-transform: uppercase;
}
.text-capitalize {
  text-transform: capitalize;
}
.text-muted {
  color: #777777;
}
.text-primary {
  color: #337ab7;
}
a.text-primary:hover,
a.text-primary:focus {
  color: #286090;
}
.text-success {
  color: #3c763d;
}
a.text-success:hover,
a.text-success:focus {
  color: #2b542c;
}
.text-info {
  color: #31708f;
}
a.text-info:hover,
a.text-info:focus {
  color: #245269;
}
.text-warning {
  color: #8a6d3b;
}
a.text-warning:hover,
a.text-warning:focus {
  color: #66512c;
}
.text-danger {
  color: #a94442;
}
a.text-danger:hover,
a.text-danger:focus {
  color: #843534;
}
.bg-primary {
  color: #fff;
  background-color: #337ab7;
}
a.bg-primary:hover,
a.bg-primary:focus {
  background-color: #286090;
}
.bg-success {
  background-color: #dff0d8;
}
a.bg-success:hover,
a.bg-success:focus {
  background-color: #c1e2b3;
}
.bg-info {
  background-color: #d9edf7;
}
a.bg-info:hover,
a.bg-info:focus {
  background-color: #afd9ee;
}
.bg-warning {
  background-color: #fcf8e3;
}
a.bg-warning:hover,
a.bg-warning:focus {
  background-color: #f7ecb5;
}
.bg-danger {
  background-color: #f2dede;
}
a.bg-danger:hover,
a.bg-danger:focus {
  background-color: #e4b9b9;
}
.page-header {
  padding-bottom: 8px;
  margin: 36px 0 18px;
  border-bottom: 1px solid #eeeeee;
}
ul,
ol {
  margin-top: 0;
  margin-bottom: 9px;
}
ul ul,
ol ul,
ul ol,
ol ol {
  margin-bottom: 0;
}
.list-unstyled {
  padding-left: 0;
  list-style: none;
}
.list-inline {
  padding-left: 0;
  list-style: none;
  margin-left: -5px;
}
.list-inline > li {
  display: inline-block;
  padding-left: 5px;
  padding-right: 5px;
}
dl {
  margin-top: 0;
  margin-bottom: 18px;
}
dt,
dd {
  line-height: 1.42857143;
}
dt {
  font-weight: bold;
}
dd {
  margin-left: 0;
}
@media (min-width: 541px) {
  .dl-horizontal dt {
    float: left;
    width: 160px;
    clear: left;
    text-align: right;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .dl-horizontal dd {
    margin-left: 180px;
  }
}
abbr[title],
abbr[data-original-title] {
  cursor: help;
  border-bottom: 1px dotted #777777;
}
.initialism {
  font-size: 90%;
  text-transform: uppercase;
}
blockquote {
  padding: 9px 18px;
  margin: 0 0 18px;
  font-size: inherit;
  border-left: 5px solid #eeeeee;
}
blockquote p:last-child,
blockquote ul:last-child,
blockquote ol:last-child {
  margin-bottom: 0;
}
blockquote footer,
blockquote small,
blockquote .small {
  display: block;
  font-size: 80%;
  line-height: 1.42857143;
  color: #777777;
}
blockquote footer:before,
blockquote small:before,
blockquote .small:before {
  content: '\2014 \00A0';
}
.blockquote-reverse,
blockquote.pull-right {
  padding-right: 15px;
  padding-left: 0;
  border-right: 5px solid #eeeeee;
  border-left: 0;
  text-align: right;
}
.blockquote-reverse footer:before,
blockquote.pull-right footer:before,
.blockquote-reverse small:before,
blockquote.pull-right small:before,
.blockquote-reverse .small:before,
blockquote.pull-right .small:before {
  content: '';
}
.blockquote-reverse footer:after,
blockquote.pull-right footer:after,
.blockquote-reverse small:after,
blockquote.pull-right small:after,
.blockquote-reverse .small:after,
blockquote.pull-right .small:after {
  content: '\00A0 \2014';
}
address {
  margin-bottom: 18px;
  font-style: normal;
  line-height: 1.42857143;
}
code,
kbd,
pre,
samp {
  font-family: monospace;
}
code {
  padding: 2px 4px;
  font-size: 90%;
  color: #c7254e;
  background-color: #f9f2f4;
  border-radius: 2px;
}
kbd {
  padding: 2px 4px;
  font-size: 90%;
  color: #888;
  background-color: transparent;
  border-radius: 1px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
}
kbd kbd {
  padding: 0;
  font-size: 100%;
  font-weight: bold;
  box-shadow: none;
}
pre {
  display: block;
  padding: 8.5px;
  margin: 0 0 9px;
  font-size: 12px;
  line-height: 1.42857143;
  word-break: break-all;
  word-wrap: break-word;
  color: #333333;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 2px;
}
pre code {
  padding: 0;
  font-size: inherit;
  color: inherit;
  white-space: pre-wrap;
  background-color: transparent;
  border-radius: 0;
}
.pre-scrollable {
  max-height: 340px;
  overflow-y: scroll;
}
.container {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
@media (min-width: 768px) {
  .container {
    width: 768px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 940px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1140px;
  }
}
.container-fluid {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
.row {
  margin-left: 0px;
  margin-right: 0px;
}
.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1, .col-xs-2, .col-sm-2, .col-md-2, .col-lg-2, .col-xs-3, .col-sm-3, .col-md-3, .col-lg-3, .col-xs-4, .col-sm-4, .col-md-4, .col-lg-4, .col-xs-5, .col-sm-5, .col-md-5, .col-lg-5, .col-xs-6, .col-sm-6, .col-md-6, .col-lg-6, .col-xs-7, .col-sm-7, .col-md-7, .col-lg-7, .col-xs-8, .col-sm-8, .col-md-8, .col-lg-8, .col-xs-9, .col-sm-9, .col-md-9, .col-lg-9, .col-xs-10, .col-sm-10, .col-md-10, .col-lg-10, .col-xs-11, .col-sm-11, .col-md-11, .col-lg-11, .col-xs-12, .col-sm-12, .col-md-12, .col-lg-12 {
  position: relative;
  min-height: 1px;
  padding-left: 0px;
  padding-right: 0px;
}
.col-xs-1, .col-xs-2, .col-xs-3, .col-xs-4, .col-xs-5, .col-xs-6, .col-xs-7, .col-xs-8, .col-xs-9, .col-xs-10, .col-xs-11, .col-xs-12 {
  float: left;
}
.col-xs-12 {
  width: 100%;
}
.col-xs-11 {
  width: 91.66666667%;
}
.col-xs-10 {
  width: 83.33333333%;
}
.col-xs-9 {
  width: 75%;
}
.col-xs-8 {
  width: 66.66666667%;
}
.col-xs-7 {
  width: 58.33333333%;
}
.col-xs-6 {
  width: 50%;
}
.col-xs-5 {
  width: 41.66666667%;
}
.col-xs-4 {
  width: 33.33333333%;
}
.col-xs-3 {
  width: 25%;
}
.col-xs-2 {
  width: 16.66666667%;
}
.col-xs-1 {
  width: 8.33333333%;
}
.col-xs-pull-12 {
  right: 100%;
}
.col-xs-pull-11 {
  right: 91.66666667%;
}
.col-xs-pull-10 {
  right: 83.33333333%;
}
.col-xs-pull-9 {
  right: 75%;
}
.col-xs-pull-8 {
  right: 66.66666667%;
}
.col-xs-pull-7 {
  right: 58.33333333%;
}
.col-xs-pull-6 {
  right: 50%;
}
.col-xs-pull-5 {
  right: 41.66666667%;
}
.col-xs-pull-4 {
  right: 33.33333333%;
}
.col-xs-pull-3 {
  right: 25%;
}
.col-xs-pull-2 {
  right: 16.66666667%;
}
.col-xs-pull-1 {
  right: 8.33333333%;
}
.col-xs-pull-0 {
  right: auto;
}
.col-xs-push-12 {
  left: 100%;
}
.col-xs-push-11 {
  left: 91.66666667%;
}
.col-xs-push-10 {
  left: 83.33333333%;
}
.col-xs-push-9 {
  left: 75%;
}
.col-xs-push-8 {
  left: 66.66666667%;
}
.col-xs-push-7 {
  left: 58.33333333%;
}
.col-xs-push-6 {
  left: 50%;
}
.col-xs-push-5 {
  left: 41.66666667%;
}
.col-xs-push-4 {
  left: 33.33333333%;
}
.col-xs-push-3 {
  left: 25%;
}
.col-xs-push-2 {
  left: 16.66666667%;
}
.col-xs-push-1 {
  left: 8.33333333%;
}
.col-xs-push-0 {
  left: auto;
}
.col-xs-offset-12 {
  margin-left: 100%;
}
.col-xs-offset-11 {
  margin-left: 91.66666667%;
}
.col-xs-offset-10 {
  margin-left: 83.33333333%;
}
.col-xs-offset-9 {
  margin-left: 75%;
}
.col-xs-offset-8 {
  margin-left: 66.66666667%;
}
.col-xs-offset-7 {
  margin-left: 58.33333333%;
}
.col-xs-offset-6 {
  margin-left: 50%;
}
.col-xs-offset-5 {
  margin-left: 41.66666667%;
}
.col-xs-offset-4 {
  margin-left: 33.33333333%;
}
.col-xs-offset-3 {
  margin-left: 25%;
}
.col-xs-offset-2 {
  margin-left: 16.66666667%;
}
.col-xs-offset-1 {
  margin-left: 8.33333333%;
}
.col-xs-offset-0 {
  margin-left: 0%;
}
@media (min-width: 768px) {
  .col-sm-1, .col-sm-2, .col-sm-3, .col-sm-4, .col-sm-5, .col-sm-6, .col-sm-7, .col-sm-8, .col-sm-9, .col-sm-10, .col-sm-11, .col-sm-12 {
    float: left;
  }
  .col-sm-12 {
    width: 100%;
  }
  .col-sm-11 {
    width: 91.66666667%;
  }
  .col-sm-10 {
    width: 83.33333333%;
  }
  .col-sm-9 {
    width: 75%;
  }
  .col-sm-8 {
    width: 66.66666667%;
  }
  .col-sm-7 {
    width: 58.33333333%;
  }
  .col-sm-6 {
    width: 50%;
  }
  .col-sm-5 {
    width: 41.66666667%;
  }
  .col-sm-4 {
    width: 33.33333333%;
  }
  .col-sm-3 {
    width: 25%;
  }
  .col-sm-2 {
    width: 16.66666667%;
  }
  .col-sm-1 {
    width: 8.33333333%;
  }
  .col-sm-pull-12 {
    right: 100%;
  }
  .col-sm-pull-11 {
    right: 91.66666667%;
  }
  .col-sm-pull-10 {
    right: 83.33333333%;
  }
  .col-sm-pull-9 {
    right: 75%;
  }
  .col-sm-pull-8 {
    right: 66.66666667%;
  }
  .col-sm-pull-7 {
    right: 58.33333333%;
  }
  .col-sm-pull-6 {
    right: 50%;
  }
  .col-sm-pull-5 {
    right: 41.66666667%;
  }
  .col-sm-pull-4 {
    right: 33.33333333%;
  }
  .col-sm-pull-3 {
    right: 25%;
  }
  .col-sm-pull-2 {
    right: 16.66666667%;
  }
  .col-sm-pull-1 {
    right: 8.33333333%;
  }
  .col-sm-pull-0 {
    right: auto;
  }
  .col-sm-push-12 {
    left: 100%;
  }
  .col-sm-push-11 {
    left: 91.66666667%;
  }
  .col-sm-push-10 {
    left: 83.33333333%;
  }
  .col-sm-push-9 {
    left: 75%;
  }
  .col-sm-push-8 {
    left: 66.66666667%;
  }
  .col-sm-push-7 {
    left: 58.33333333%;
  }
  .col-sm-push-6 {
    left: 50%;
  }
  .col-sm-push-5 {
    left: 41.66666667%;
  }
  .col-sm-push-4 {
    left: 33.33333333%;
  }
  .col-sm-push-3 {
    left: 25%;
  }
  .col-sm-push-2 {
    left: 16.66666667%;
  }
  .col-sm-push-1 {
    left: 8.33333333%;
  }
  .col-sm-push-0 {
    left: auto;
  }
  .col-sm-offset-12 {
    margin-left: 100%;
  }
  .col-sm-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-sm-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-sm-offset-9 {
    margin-left: 75%;
  }
  .col-sm-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-sm-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-sm-offset-6 {
    margin-left: 50%;
  }
  .col-sm-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-sm-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-sm-offset-3 {
    margin-left: 25%;
  }
  .col-sm-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-sm-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-sm-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 992px) {
  .col-md-1, .col-md-2, .col-md-3, .col-md-4, .col-md-5, .col-md-6, .col-md-7, .col-md-8, .col-md-9, .col-md-10, .col-md-11, .col-md-12 {
    float: left;
  }
  .col-md-12 {
    width: 100%;
  }
  .col-md-11 {
    width: 91.66666667%;
  }
  .col-md-10 {
    width: 83.33333333%;
  }
  .col-md-9 {
    width: 75%;
  }
  .col-md-8 {
    width: 66.66666667%;
  }
  .col-md-7 {
    width: 58.33333333%;
  }
  .col-md-6 {
    width: 50%;
  }
  .col-md-5 {
    width: 41.66666667%;
  }
  .col-md-4 {
    width: 33.33333333%;
  }
  .col-md-3 {
    width: 25%;
  }
  .col-md-2 {
    width: 16.66666667%;
  }
  .col-md-1 {
    width: 8.33333333%;
  }
  .col-md-pull-12 {
    right: 100%;
  }
  .col-md-pull-11 {
    right: 91.66666667%;
  }
  .col-md-pull-10 {
    right: 83.33333333%;
  }
  .col-md-pull-9 {
    right: 75%;
  }
  .col-md-pull-8 {
    right: 66.66666667%;
  }
  .col-md-pull-7 {
    right: 58.33333333%;
  }
  .col-md-pull-6 {
    right: 50%;
  }
  .col-md-pull-5 {
    right: 41.66666667%;
  }
  .col-md-pull-4 {
    right: 33.33333333%;
  }
  .col-md-pull-3 {
    right: 25%;
  }
  .col-md-pull-2 {
    right: 16.66666667%;
  }
  .col-md-pull-1 {
    right: 8.33333333%;
  }
  .col-md-pull-0 {
    right: auto;
  }
  .col-md-push-12 {
    left: 100%;
  }
  .col-md-push-11 {
    left: 91.66666667%;
  }
  .col-md-push-10 {
    left: 83.33333333%;
  }
  .col-md-push-9 {
    left: 75%;
  }
  .col-md-push-8 {
    left: 66.66666667%;
  }
  .col-md-push-7 {
    left: 58.33333333%;
  }
  .col-md-push-6 {
    left: 50%;
  }
  .col-md-push-5 {
    left: 41.66666667%;
  }
  .col-md-push-4 {
    left: 33.33333333%;
  }
  .col-md-push-3 {
    left: 25%;
  }
  .col-md-push-2 {
    left: 16.66666667%;
  }
  .col-md-push-1 {
    left: 8.33333333%;
  }
  .col-md-push-0 {
    left: auto;
  }
  .col-md-offset-12 {
    margin-left: 100%;
  }
  .col-md-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-md-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-md-offset-9 {
    margin-left: 75%;
  }
  .col-md-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-md-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-md-offset-6 {
    margin-left: 50%;
  }
  .col-md-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-md-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-md-offset-3 {
    margin-left: 25%;
  }
  .col-md-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-md-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-md-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 1200px) {
  .col-lg-1, .col-lg-2, .col-lg-3, .col-lg-4, .col-lg-5, .col-lg-6, .col-lg-7, .col-lg-8, .col-lg-9, .col-lg-10, .col-lg-11, .col-lg-12 {
    float: left;
  }
  .col-lg-12 {
    width: 100%;
  }
  .col-lg-11 {
    width: 91.66666667%;
  }
  .col-lg-10 {
    width: 83.33333333%;
  }
  .col-lg-9 {
    width: 75%;
  }
  .col-lg-8 {
    width: 66.66666667%;
  }
  .col-lg-7 {
    width: 58.33333333%;
  }
  .col-lg-6 {
    width: 50%;
  }
  .col-lg-5 {
    width: 41.66666667%;
  }
  .col-lg-4 {
    width: 33.33333333%;
  }
  .col-lg-3 {
    width: 25%;
  }
  .col-lg-2 {
    width: 16.66666667%;
  }
  .col-lg-1 {
    width: 8.33333333%;
  }
  .col-lg-pull-12 {
    right: 100%;
  }
  .col-lg-pull-11 {
    right: 91.66666667%;
  }
  .col-lg-pull-10 {
    right: 83.33333333%;
  }
  .col-lg-pull-9 {
    right: 75%;
  }
  .col-lg-pull-8 {
    right: 66.66666667%;
  }
  .col-lg-pull-7 {
    right: 58.33333333%;
  }
  .col-lg-pull-6 {
    right: 50%;
  }
  .col-lg-pull-5 {
    right: 41.66666667%;
  }
  .col-lg-pull-4 {
    right: 33.33333333%;
  }
  .col-lg-pull-3 {
    right: 25%;
  }
  .col-lg-pull-2 {
    right: 16.66666667%;
  }
  .col-lg-pull-1 {
    right: 8.33333333%;
  }
  .col-lg-pull-0 {
    right: auto;
  }
  .col-lg-push-12 {
    left: 100%;
  }
  .col-lg-push-11 {
    left: 91.66666667%;
  }
  .col-lg-push-10 {
    left: 83.33333333%;
  }
  .col-lg-push-9 {
    left: 75%;
  }
  .col-lg-push-8 {
    left: 66.66666667%;
  }
  .col-lg-push-7 {
    left: 58.33333333%;
  }
  .col-lg-push-6 {
    left: 50%;
  }
  .col-lg-push-5 {
    left: 41.66666667%;
  }
  .col-lg-push-4 {
    left: 33.33333333%;
  }
  .col-lg-push-3 {
    left: 25%;
  }
  .col-lg-push-2 {
    left: 16.66666667%;
  }
  .col-lg-push-1 {
    left: 8.33333333%;
  }
  .col-lg-push-0 {
    left: auto;
  }
  .col-lg-offset-12 {
    margin-left: 100%;
  }
  .col-lg-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-lg-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-lg-offset-9 {
    margin-left: 75%;
  }
  .col-lg-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-lg-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-lg-offset-6 {
    margin-left: 50%;
  }
  .col-lg-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-lg-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-lg-offset-3 {
    margin-left: 25%;
  }
  .col-lg-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-lg-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-lg-offset-0 {
    margin-left: 0%;
  }
}
table {
  background-color: transparent;
}
caption {
  padding-top: 8px;
  padding-bottom: 8px;
  color: #777777;
  text-align: left;
}
th {
  text-align: left;
}
.table {
  width: 100%;
  max-width: 100%;
  margin-bottom: 18px;
}
.table > thead > tr > th,
.table > tbody > tr > th,
.table > tfoot > tr > th,
.table > thead > tr > td,
.table > tbody > tr > td,
.table > tfoot > tr > td {
  padding: 8px;
  line-height: 1.42857143;
  vertical-align: top;
  border-top: 1px solid #ddd;
}
.table > thead > tr > th {
  vertical-align: bottom;
  border-bottom: 2px solid #ddd;
}
.table > caption + thead > tr:first-child > th,
.table > colgroup + thead > tr:first-child > th,
.table > thead:first-child > tr:first-child > th,
.table > caption + thead > tr:first-child > td,
.table > colgroup + thead > tr:first-child > td,
.table > thead:first-child > tr:first-child > td {
  border-top: 0;
}
.table > tbody + tbody {
  border-top: 2px solid #ddd;
}
.table .table {
  background-color: #fff;
}
.table-condensed > thead > tr > th,
.table-condensed > tbody > tr > th,
.table-condensed > tfoot > tr > th,
.table-condensed > thead > tr > td,
.table-condensed > tbody > tr > td,
.table-condensed > tfoot > tr > td {
  padding: 5px;
}
.table-bordered {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > tbody > tr > th,
.table-bordered > tfoot > tr > th,
.table-bordered > thead > tr > td,
.table-bordered > tbody > tr > td,
.table-bordered > tfoot > tr > td {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > thead > tr > td {
  border-bottom-width: 2px;
}
.table-striped > tbody > tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}
.table-hover > tbody > tr:hover {
  background-color: #f5f5f5;
}
table col[class*="col-"] {
  position: static;
  float: none;
  display: table-column;
}
table td[class*="col-"],
table th[class*="col-"] {
  position: static;
  float: none;
  display: table-cell;
}
.table > thead > tr > td.active,
.table > tbody > tr > td.active,
.table > tfoot > tr > td.active,
.table > thead > tr > th.active,
.table > tbody > tr > th.active,
.table > tfoot > tr > th.active,
.table > thead > tr.active > td,
.table > tbody > tr.active > td,
.table > tfoot > tr.active > td,
.table > thead > tr.active > th,
.table > tbody > tr.active > th,
.table > tfoot > tr.active > th {
  background-color: #f5f5f5;
}
.table-hover > tbody > tr > td.active:hover,
.table-hover > tbody > tr > th.active:hover,
.table-hover > tbody > tr.active:hover > td,
.table-hover > tbody > tr:hover > .active,
.table-hover > tbody > tr.active:hover > th {
  background-color: #e8e8e8;
}
.table > thead > tr > td.success,
.table > tbody > tr > td.success,
.table > tfoot > tr > td.success,
.table > thead > tr > th.success,
.table > tbody > tr > th.success,
.table > tfoot > tr > th.success,
.table > thead > tr.success > td,
.table > tbody > tr.success > td,
.table > tfoot > tr.success > td,
.table > thead > tr.success > th,
.table > tbody > tr.success > th,
.table > tfoot > tr.success > th {
  background-color: #dff0d8;
}
.table-hover > tbody > tr > td.success:hover,
.table-hover > tbody > tr > th.success:hover,
.table-hover > tbody > tr.success:hover > td,
.table-hover > tbody > tr:hover > .success,
.table-hover > tbody > tr.success:hover > th {
  background-color: #d0e9c6;
}
.table > thead > tr > td.info,
.table > tbody > tr > td.info,
.table > tfoot > tr > td.info,
.table > thead > tr > th.info,
.table > tbody > tr > th.info,
.table > tfoot > tr > th.info,
.table > thead > tr.info > td,
.table > tbody > tr.info > td,
.table > tfoot > tr.info > td,
.table > thead > tr.info > th,
.table > tbody > tr.info > th,
.table > tfoot > tr.info > th {
  background-color: #d9edf7;
}
.table-hover > tbody > tr > td.info:hover,
.table-hover > tbody > tr > th.info:hover,
.table-hover > tbody > tr.info:hover > td,
.table-hover > tbody > tr:hover > .info,
.table-hover > tbody > tr.info:hover > th {
  background-color: #c4e3f3;
}
.table > thead > tr > td.warning,
.table > tbody > tr > td.warning,
.table > tfoot > tr > td.warning,
.table > thead > tr > th.warning,
.table > tbody > tr > th.warning,
.table > tfoot > tr > th.warning,
.table > thead > tr.warning > td,
.table > tbody > tr.warning > td,
.table > tfoot > tr.warning > td,
.table > thead > tr.warning > th,
.table > tbody > tr.warning > th,
.table > tfoot > tr.warning > th {
  background-color: #fcf8e3;
}
.table-hover > tbody > tr > td.warning:hover,
.table-hover > tbody > tr > th.warning:hover,
.table-hover > tbody > tr.warning:hover > td,
.table-hover > tbody > tr:hover > .warning,
.table-hover > tbody > tr.warning:hover > th {
  background-color: #faf2cc;
}
.table > thead > tr > td.danger,
.table > tbody > tr > td.danger,
.table > tfoot > tr > td.danger,
.table > thead > tr > th.danger,
.table > tbody > tr > th.danger,
.table > tfoot > tr > th.danger,
.table > thead > tr.danger > td,
.table > tbody > tr.danger > td,
.table > tfoot > tr.danger > td,
.table > thead > tr.danger > th,
.table > tbody > tr.danger > th,
.table > tfoot > tr.danger > th {
  background-color: #f2dede;
}
.table-hover > tbody > tr > td.danger:hover,
.table-hover > tbody > tr > th.danger:hover,
.table-hover > tbody > tr.danger:hover > td,
.table-hover > tbody > tr:hover > .danger,
.table-hover > tbody > tr.danger:hover > th {
  background-color: #ebcccc;
}
.table-responsive {
  overflow-x: auto;
  min-height: 0.01%;
}
@media screen and (max-width: 767px) {
  .table-responsive {
    width: 100%;
    margin-bottom: 13.5px;
    overflow-y: hidden;
    -ms-overflow-style: -ms-autohiding-scrollbar;
    border: 1px solid #ddd;
  }
  .table-responsive > .table {
    margin-bottom: 0;
  }
  .table-responsive > .table > thead > tr > th,
  .table-responsive > .table > tbody > tr > th,
  .table-responsive > .table > tfoot > tr > th,
  .table-responsive > .table > thead > tr > td,
  .table-responsive > .table > tbody > tr > td,
  .table-responsive > .table > tfoot > tr > td {
    white-space: nowrap;
  }
  .table-responsive > .table-bordered {
    border: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:first-child,
  .table-responsive > .table-bordered > tbody > tr > th:first-child,
  .table-responsive > .table-bordered > tfoot > tr > th:first-child,
  .table-responsive > .table-bordered > thead > tr > td:first-child,
  .table-responsive > .table-bordered > tbody > tr > td:first-child,
  .table-responsive > .table-bordered > tfoot > tr > td:first-child {
    border-left: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:last-child,
  .table-responsive > .table-bordered > tbody > tr > th:last-child,
  .table-responsive > .table-bordered > tfoot > tr > th:last-child,
  .table-responsive > .table-bordered > thead > tr > td:last-child,
  .table-responsive > .table-bordered > tbody > tr > td:last-child,
  .table-responsive > .table-bordered > tfoot > tr > td:last-child {
    border-right: 0;
  }
  .table-responsive > .table-bordered > tbody > tr:last-child > th,
  .table-responsive > .table-bordered > tfoot > tr:last-child > th,
  .table-responsive > .table-bordered > tbody > tr:last-child > td,
  .table-responsive > .table-bordered > tfoot > tr:last-child > td {
    border-bottom: 0;
  }
}
fieldset {
  padding: 0;
  margin: 0;
  border: 0;
  min-width: 0;
}
legend {
  display: block;
  width: 100%;
  padding: 0;
  margin-bottom: 18px;
  font-size: 19.5px;
  line-height: inherit;
  color: #333333;
  border: 0;
  border-bottom: 1px solid #e5e5e5;
}
label {
  display: inline-block;
  max-width: 100%;
  margin-bottom: 5px;
  font-weight: bold;
}
input[type="search"] {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
input[type="radio"],
input[type="checkbox"] {
  margin: 4px 0 0;
  margin-top: 1px \9;
  line-height: normal;
}
input[type="file"] {
  display: block;
}
input[type="range"] {
  display: block;
  width: 100%;
}
select[multiple],
select[size] {
  height: auto;
}
input[type="file"]:focus,
input[type="radio"]:focus,
input[type="checkbox"]:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
output {
  display: block;
  padding-top: 7px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
}
.form-control {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
}
.form-control:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.form-control::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.form-control:-ms-input-placeholder {
  color: #999;
}
.form-control::-webkit-input-placeholder {
  color: #999;
}
.form-control::-ms-expand {
  border: 0;
  background-color: transparent;
}
.form-control[disabled],
.form-control[readonly],
fieldset[disabled] .form-control {
  background-color: #eeeeee;
  opacity: 1;
}
.form-control[disabled],
fieldset[disabled] .form-control {
  cursor: not-allowed;
}
textarea.form-control {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: none;
}
@media screen and (-webkit-min-device-pixel-ratio: 0) {
  input[type="date"].form-control,
  input[type="time"].form-control,
  input[type="datetime-local"].form-control,
  input[type="month"].form-control {
    line-height: 32px;
  }
  input[type="date"].input-sm,
  input[type="time"].input-sm,
  input[type="datetime-local"].input-sm,
  input[type="month"].input-sm,
  .input-group-sm input[type="date"],
  .input-group-sm input[type="time"],
  .input-group-sm input[type="datetime-local"],
  .input-group-sm input[type="month"] {
    line-height: 30px;
  }
  input[type="date"].input-lg,
  input[type="time"].input-lg,
  input[type="datetime-local"].input-lg,
  input[type="month"].input-lg,
  .input-group-lg input[type="date"],
  .input-group-lg input[type="time"],
  .input-group-lg input[type="datetime-local"],
  .input-group-lg input[type="month"] {
    line-height: 45px;
  }
}
.form-group {
  margin-bottom: 15px;
}
.radio,
.checkbox {
  position: relative;
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}
.radio label,
.checkbox label {
  min-height: 18px;
  padding-left: 20px;
  margin-bottom: 0;
  font-weight: normal;
  cursor: pointer;
}
.radio input[type="radio"],
.radio-inline input[type="radio"],
.checkbox input[type="checkbox"],
.checkbox-inline input[type="checkbox"] {
  position: absolute;
  margin-left: -20px;
  margin-top: 4px \9;
}
.radio + .radio,
.checkbox + .checkbox {
  margin-top: -5px;
}
.radio-inline,
.checkbox-inline {
  position: relative;
  display: inline-block;
  padding-left: 20px;
  margin-bottom: 0;
  vertical-align: middle;
  font-weight: normal;
  cursor: pointer;
}
.radio-inline + .radio-inline,
.checkbox-inline + .checkbox-inline {
  margin-top: 0;
  margin-left: 10px;
}
input[type="radio"][disabled],
input[type="checkbox"][disabled],
input[type="radio"].disabled,
input[type="checkbox"].disabled,
fieldset[disabled] input[type="radio"],
fieldset[disabled] input[type="checkbox"] {
  cursor: not-allowed;
}
.radio-inline.disabled,
.checkbox-inline.disabled,
fieldset[disabled] .radio-inline,
fieldset[disabled] .checkbox-inline {
  cursor: not-allowed;
}
.radio.disabled label,
.checkbox.disabled label,
fieldset[disabled] .radio label,
fieldset[disabled] .checkbox label {
  cursor: not-allowed;
}
.form-control-static {
  padding-top: 7px;
  padding-bottom: 7px;
  margin-bottom: 0;
  min-height: 31px;
}
.form-control-static.input-lg,
.form-control-static.input-sm {
  padding-left: 0;
  padding-right: 0;
}
.input-sm {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-sm {
  height: 30px;
  line-height: 30px;
}
textarea.input-sm,
select[multiple].input-sm {
  height: auto;
}
.form-group-sm .form-control {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.form-group-sm select.form-control {
  height: 30px;
  line-height: 30px;
}
.form-group-sm textarea.form-control,
.form-group-sm select[multiple].form-control {
  height: auto;
}
.form-group-sm .form-control-static {
  height: 30px;
  min-height: 30px;
  padding: 6px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.input-lg {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-lg {
  height: 45px;
  line-height: 45px;
}
textarea.input-lg,
select[multiple].input-lg {
  height: auto;
}
.form-group-lg .form-control {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.form-group-lg select.form-control {
  height: 45px;
  line-height: 45px;
}
.form-group-lg textarea.form-control,
.form-group-lg select[multiple].form-control {
  height: auto;
}
.form-group-lg .form-control-static {
  height: 45px;
  min-height: 35px;
  padding: 11px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.has-feedback {
  position: relative;
}
.has-feedback .form-control {
  padding-right: 40px;
}
.form-control-feedback {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 2;
  display: block;
  width: 32px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  pointer-events: none;
}
.input-lg + .form-control-feedback,
.input-group-lg + .form-control-feedback,
.form-group-lg .form-control + .form-control-feedback {
  width: 45px;
  height: 45px;
  line-height: 45px;
}
.input-sm + .form-control-feedback,
.input-group-sm + .form-control-feedback,
.form-group-sm .form-control + .form-control-feedback {
  width: 30px;
  height: 30px;
  line-height: 30px;
}
.has-success .help-block,
.has-success .control-label,
.has-success .radio,
.has-success .checkbox,
.has-success .radio-inline,
.has-success .checkbox-inline,
.has-success.radio label,
.has-success.checkbox label,
.has-success.radio-inline label,
.has-success.checkbox-inline label {
  color: #3c763d;
}
.has-success .form-control {
  border-color: #3c763d;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-success .form-control:focus {
  border-color: #2b542c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
}
.has-success .input-group-addon {
  color: #3c763d;
  border-color: #3c763d;
  background-color: #dff0d8;
}
.has-success .form-control-feedback {
  color: #3c763d;
}
.has-warning .help-block,
.has-warning .control-label,
.has-warning .radio,
.has-warning .checkbox,
.has-warning .radio-inline,
.has-warning .checkbox-inline,
.has-warning.radio label,
.has-warning.checkbox label,
.has-warning.radio-inline label,
.has-warning.checkbox-inline label {
  color: #8a6d3b;
}
.has-warning .form-control {
  border-color: #8a6d3b;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-warning .form-control:focus {
  border-color: #66512c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
}
.has-warning .input-group-addon {
  color: #8a6d3b;
  border-color: #8a6d3b;
  background-color: #fcf8e3;
}
.has-warning .form-control-feedback {
  color: #8a6d3b;
}
.has-error .help-block,
.has-error .control-label,
.has-error .radio,
.has-error .checkbox,
.has-error .radio-inline,
.has-error .checkbox-inline,
.has-error.radio label,
.has-error.checkbox label,
.has-error.radio-inline label,
.has-error.checkbox-inline label {
  color: #a94442;
}
.has-error .form-control {
  border-color: #a94442;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-error .form-control:focus {
  border-color: #843534;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
}
.has-error .input-group-addon {
  color: #a94442;
  border-color: #a94442;
  background-color: #f2dede;
}
.has-error .form-control-feedback {
  color: #a94442;
}
.has-feedback label ~ .form-control-feedback {
  top: 23px;
}
.has-feedback label.sr-only ~ .form-control-feedback {
  top: 0;
}
.help-block {
  display: block;
  margin-top: 5px;
  margin-bottom: 10px;
  color: #404040;
}
@media (min-width: 768px) {
  .form-inline .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .form-inline .form-control-static {
    display: inline-block;
  }
  .form-inline .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .form-inline .input-group .input-group-addon,
  .form-inline .input-group .input-group-btn,
  .form-inline .input-group .form-control {
    width: auto;
  }
  .form-inline .input-group > .form-control {
    width: 100%;
  }
  .form-inline .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio,
  .form-inline .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio label,
  .form-inline .checkbox label {
    padding-left: 0;
  }
  .form-inline .radio input[type="radio"],
  .form-inline .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .form-inline .has-feedback .form-control-feedback {
    top: 0;
  }
}
.form-horizontal .radio,
.form-horizontal .checkbox,
.form-horizontal .radio-inline,
.form-horizontal .checkbox-inline {
  margin-top: 0;
  margin-bottom: 0;
  padding-top: 7px;
}
.form-horizontal .radio,
.form-horizontal .checkbox {
  min-height: 25px;
}
.form-horizontal .form-group {
  margin-left: 0px;
  margin-right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .control-label {
    text-align: right;
    margin-bottom: 0;
    padding-top: 7px;
  }
}
.form-horizontal .has-feedback .form-control-feedback {
  right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .form-group-lg .control-label {
    padding-top: 11px;
    font-size: 17px;
  }
}
@media (min-width: 768px) {
  .form-horizontal .form-group-sm .control-label {
    padding-top: 6px;
    font-size: 12px;
  }
}
.btn {
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  white-space: nowrap;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  border-radius: 2px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
.btn:hover,
.btn:focus,
.btn.focus {
  color: #333;
  text-decoration: none;
}
.btn:active,
.btn.active {
  outline: 0;
  background-image: none;
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
  cursor: not-allowed;
  opacity: 0.65;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
  box-shadow: none;
}
a.btn.disabled,
fieldset[disabled] a.btn {
  pointer-events: none;
}
.btn-default {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.btn-default:focus,
.btn-default.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.btn-default:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active:hover,
.btn-default.active:hover,
.open > .dropdown-toggle.btn-default:hover,
.btn-default:active:focus,
.btn-default.active:focus,
.open > .dropdown-toggle.btn-default:focus,
.btn-default:active.focus,
.btn-default.active.focus,
.open > .dropdown-toggle.btn-default.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  background-image: none;
}
.btn-default.disabled:hover,
.btn-default[disabled]:hover,
fieldset[disabled] .btn-default:hover,
.btn-default.disabled:focus,
.btn-default[disabled]:focus,
fieldset[disabled] .btn-default:focus,
.btn-default.disabled.focus,
.btn-default[disabled].focus,
fieldset[disabled] .btn-default.focus {
  background-color: #fff;
  border-color: #ccc;
}
.btn-default .badge {
  color: #fff;
  background-color: #333;
}
.btn-primary {
  color: #fff;
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary:focus,
.btn-primary.focus {
  color: #fff;
  background-color: #286090;
  border-color: #122b40;
}
.btn-primary:hover {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active:hover,
.btn-primary.active:hover,
.open > .dropdown-toggle.btn-primary:hover,
.btn-primary:active:focus,
.btn-primary.active:focus,
.open > .dropdown-toggle.btn-primary:focus,
.btn-primary:active.focus,
.btn-primary.active.focus,
.open > .dropdown-toggle.btn-primary.focus {
  color: #fff;
  background-color: #204d74;
  border-color: #122b40;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  background-image: none;
}
.btn-primary.disabled:hover,
.btn-primary[disabled]:hover,
fieldset[disabled] .btn-primary:hover,
.btn-primary.disabled:focus,
.btn-primary[disabled]:focus,
fieldset[disabled] .btn-primary:focus,
.btn-primary.disabled.focus,
.btn-primary[disabled].focus,
fieldset[disabled] .btn-primary.focus {
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary .badge {
  color: #337ab7;
  background-color: #fff;
}
.btn-success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success:focus,
.btn-success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.btn-success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active:hover,
.btn-success.active:hover,
.open > .dropdown-toggle.btn-success:hover,
.btn-success:active:focus,
.btn-success.active:focus,
.open > .dropdown-toggle.btn-success:focus,
.btn-success:active.focus,
.btn-success.active.focus,
.open > .dropdown-toggle.btn-success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  background-image: none;
}
.btn-success.disabled:hover,
.btn-success[disabled]:hover,
fieldset[disabled] .btn-success:hover,
.btn-success.disabled:focus,
.btn-success[disabled]:focus,
fieldset[disabled] .btn-success:focus,
.btn-success.disabled.focus,
.btn-success[disabled].focus,
fieldset[disabled] .btn-success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.btn-info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info:focus,
.btn-info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.btn-info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active:hover,
.btn-info.active:hover,
.open > .dropdown-toggle.btn-info:hover,
.btn-info:active:focus,
.btn-info.active:focus,
.open > .dropdown-toggle.btn-info:focus,
.btn-info:active.focus,
.btn-info.active.focus,
.open > .dropdown-toggle.btn-info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  background-image: none;
}
.btn-info.disabled:hover,
.btn-info[disabled]:hover,
fieldset[disabled] .btn-info:hover,
.btn-info.disabled:focus,
.btn-info[disabled]:focus,
fieldset[disabled] .btn-info:focus,
.btn-info.disabled.focus,
.btn-info[disabled].focus,
fieldset[disabled] .btn-info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.btn-warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning:focus,
.btn-warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.btn-warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active:hover,
.btn-warning.active:hover,
.open > .dropdown-toggle.btn-warning:hover,
.btn-warning:active:focus,
.btn-warning.active:focus,
.open > .dropdown-toggle.btn-warning:focus,
.btn-warning:active.focus,
.btn-warning.active.focus,
.open > .dropdown-toggle.btn-warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  background-image: none;
}
.btn-warning.disabled:hover,
.btn-warning[disabled]:hover,
fieldset[disabled] .btn-warning:hover,
.btn-warning.disabled:focus,
.btn-warning[disabled]:focus,
fieldset[disabled] .btn-warning:focus,
.btn-warning.disabled.focus,
.btn-warning[disabled].focus,
fieldset[disabled] .btn-warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.btn-danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger:focus,
.btn-danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.btn-danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active:hover,
.btn-danger.active:hover,
.open > .dropdown-toggle.btn-danger:hover,
.btn-danger:active:focus,
.btn-danger.active:focus,
.open > .dropdown-toggle.btn-danger:focus,
.btn-danger:active.focus,
.btn-danger.active.focus,
.open > .dropdown-toggle.btn-danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  background-image: none;
}
.btn-danger.disabled:hover,
.btn-danger[disabled]:hover,
fieldset[disabled] .btn-danger:hover,
.btn-danger.disabled:focus,
.btn-danger[disabled]:focus,
fieldset[disabled] .btn-danger:focus,
.btn-danger.disabled.focus,
.btn-danger[disabled].focus,
fieldset[disabled] .btn-danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger .badge {
  color: #d9534f;
  background-color: #fff;
}
.btn-link {
  color: #337ab7;
  font-weight: normal;
  border-radius: 0;
}
.btn-link,
.btn-link:active,
.btn-link.active,
.btn-link[disabled],
fieldset[disabled] .btn-link {
  background-color: transparent;
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn-link,
.btn-link:hover,
.btn-link:focus,
.btn-link:active {
  border-color: transparent;
}
.btn-link:hover,
.btn-link:focus {
  color: #23527c;
  text-decoration: underline;
  background-color: transparent;
}
.btn-link[disabled]:hover,
fieldset[disabled] .btn-link:hover,
.btn-link[disabled]:focus,
fieldset[disabled] .btn-link:focus {
  color: #777777;
  text-decoration: none;
}
.btn-lg,
.btn-group-lg > .btn {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.btn-sm,
.btn-group-sm > .btn {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-xs,
.btn-group-xs > .btn {
  padding: 1px 5px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-block {
  display: block;
  width: 100%;
}
.btn-block + .btn-block {
  margin-top: 5px;
}
input[type="submit"].btn-block,
input[type="reset"].btn-block,
input[type="button"].btn-block {
  width: 100%;
}
.fade {
  opacity: 0;
  -webkit-transition: opacity 0.15s linear;
  -o-transition: opacity 0.15s linear;
  transition: opacity 0.15s linear;
}
.fade.in {
  opacity: 1;
}
.collapse {
  display: none;
}
.collapse.in {
  display: block;
}
tr.collapse.in {
  display: table-row;
}
tbody.collapse.in {
  display: table-row-group;
}
.collapsing {
  position: relative;
  height: 0;
  overflow: hidden;
  -webkit-transition-property: height, visibility;
  transition-property: height, visibility;
  -webkit-transition-duration: 0.35s;
  transition-duration: 0.35s;
  -webkit-transition-timing-function: ease;
  transition-timing-function: ease;
}
.caret {
  display: inline-block;
  width: 0;
  height: 0;
  margin-left: 2px;
  vertical-align: middle;
  border-top: 4px dashed;
  border-top: 4px solid \9;
  border-right: 4px solid transparent;
  border-left: 4px solid transparent;
}
.dropup,
.dropdown {
  position: relative;
}
.dropdown-toggle:focus {
  outline: 0;
}
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1000;
  display: none;
  float: left;
  min-width: 160px;
  padding: 5px 0;
  margin: 2px 0 0;
  list-style: none;
  font-size: 13px;
  text-align: left;
  background-color: #fff;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.15);
  border-radius: 2px;
  -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  background-clip: padding-box;
}
.dropdown-menu.pull-right {
  right: 0;
  left: auto;
}
.dropdown-menu .divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.dropdown-menu > li > a {
  display: block;
  padding: 3px 20px;
  clear: both;
  font-weight: normal;
  line-height: 1.42857143;
  color: #333333;
  white-space: nowrap;
}
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus {
  text-decoration: none;
  color: #262626;
  background-color: #f5f5f5;
}
.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus {
  color: #fff;
  text-decoration: none;
  outline: 0;
  background-color: #337ab7;
}
.dropdown-menu > .disabled > a,
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  color: #777777;
}
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  text-decoration: none;
  background-color: transparent;
  background-image: none;
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
  cursor: not-allowed;
}
.open > .dropdown-menu {
  display: block;
}
.open > a {
  outline: 0;
}
.dropdown-menu-right {
  left: auto;
  right: 0;
}
.dropdown-menu-left {
  left: 0;
  right: auto;
}
.dropdown-header {
  display: block;
  padding: 3px 20px;
  font-size: 12px;
  line-height: 1.42857143;
  color: #777777;
  white-space: nowrap;
}
.dropdown-backdrop {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  z-index: 990;
}
.pull-right > .dropdown-menu {
  right: 0;
  left: auto;
}
.dropup .caret,
.navbar-fixed-bottom .dropdown .caret {
  border-top: 0;
  border-bottom: 4px dashed;
  border-bottom: 4px solid \9;
  content: "";
}
.dropup .dropdown-menu,
.navbar-fixed-bottom .dropdown .dropdown-menu {
  top: auto;
  bottom: 100%;
  margin-bottom: 2px;
}
@media (min-width: 541px) {
  .navbar-right .dropdown-menu {
    left: auto;
    right: 0;
  }
  .navbar-right .dropdown-menu-left {
    left: 0;
    right: auto;
  }
}
.btn-group,
.btn-group-vertical {
  position: relative;
  display: inline-block;
  vertical-align: middle;
}
.btn-group > .btn,
.btn-group-vertical > .btn {
  position: relative;
  float: left;
}
.btn-group > .btn:hover,
.btn-group-vertical > .btn:hover,
.btn-group > .btn:focus,
.btn-group-vertical > .btn:focus,
.btn-group > .btn:active,
.btn-group-vertical > .btn:active,
.btn-group > .btn.active,
.btn-group-vertical > .btn.active {
  z-index: 2;
}
.btn-group .btn + .btn,
.btn-group .btn + .btn-group,
.btn-group .btn-group + .btn,
.btn-group .btn-group + .btn-group {
  margin-left: -1px;
}
.btn-toolbar {
  margin-left: -5px;
}
.btn-toolbar .btn,
.btn-toolbar .btn-group,
.btn-toolbar .input-group {
  float: left;
}
.btn-toolbar > .btn,
.btn-toolbar > .btn-group,
.btn-toolbar > .input-group {
  margin-left: 5px;
}
.btn-group > .btn:not(:first-child):not(:last-child):not(.dropdown-toggle) {
  border-radius: 0;
}
.btn-group > .btn:first-child {
  margin-left: 0;
}
.btn-group > .btn:first-child:not(:last-child):not(.dropdown-toggle) {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn:last-child:not(:first-child),
.btn-group > .dropdown-toggle:not(:first-child) {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group > .btn-group {
  float: left;
}
.btn-group > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group .dropdown-toggle:active,
.btn-group.open .dropdown-toggle {
  outline: 0;
}
.btn-group > .btn + .dropdown-toggle {
  padding-left: 8px;
  padding-right: 8px;
}
.btn-group > .btn-lg + .dropdown-toggle {
  padding-left: 12px;
  padding-right: 12px;
}
.btn-group.open .dropdown-toggle {
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn-group.open .dropdown-toggle.btn-link {
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn .caret {
  margin-left: 0;
}
.btn-lg .caret {
  border-width: 5px 5px 0;
  border-bottom-width: 0;
}
.dropup .btn-lg .caret {
  border-width: 0 5px 5px;
}
.btn-group-vertical > .btn,
.btn-group-vertical > .btn-group,
.btn-group-vertical > .btn-group > .btn {
  display: block;
  float: none;
  width: 100%;
  max-width: 100%;
}
.btn-group-vertical > .btn-group > .btn {
  float: none;
}
.btn-group-vertical > .btn + .btn,
.btn-group-vertical > .btn + .btn-group,
.btn-group-vertical > .btn-group + .btn,
.btn-group-vertical > .btn-group + .btn-group {
  margin-top: -1px;
  margin-left: 0;
}
.btn-group-vertical > .btn:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.btn-group-vertical > .btn:first-child:not(:last-child) {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn:last-child:not(:first-child) {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
.btn-group-vertical > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.btn-group-justified {
  display: table;
  width: 100%;
  table-layout: fixed;
  border-collapse: separate;
}
.btn-group-justified > .btn,
.btn-group-justified > .btn-group {
  float: none;
  display: table-cell;
  width: 1%;
}
.btn-group-justified > .btn-group .btn {
  width: 100%;
}
.btn-group-justified > .btn-group .dropdown-menu {
  left: auto;
}
[data-toggle="buttons"] > .btn input[type="radio"],
[data-toggle="buttons"] > .btn-group > .btn input[type="radio"],
[data-toggle="buttons"] > .btn input[type="checkbox"],
[data-toggle="buttons"] > .btn-group > .btn input[type="checkbox"] {
  position: absolute;
  clip: rect(0, 0, 0, 0);
  pointer-events: none;
}
.input-group {
  position: relative;
  display: table;
  border-collapse: separate;
}
.input-group[class*="col-"] {
  float: none;
  padding-left: 0;
  padding-right: 0;
}
.input-group .form-control {
  position: relative;
  z-index: 2;
  float: left;
  width: 100%;
  margin-bottom: 0;
}
.input-group .form-control:focus {
  z-index: 3;
}
.input-group-lg > .form-control,
.input-group-lg > .input-group-addon,
.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-group-lg > .form-control,
select.input-group-lg > .input-group-addon,
select.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  line-height: 45px;
}
textarea.input-group-lg > .form-control,
textarea.input-group-lg > .input-group-addon,
textarea.input-group-lg > .input-group-btn > .btn,
select[multiple].input-group-lg > .form-control,
select[multiple].input-group-lg > .input-group-addon,
select[multiple].input-group-lg > .input-group-btn > .btn {
  height: auto;
}
.input-group-sm > .form-control,
.input-group-sm > .input-group-addon,
.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-group-sm > .form-control,
select.input-group-sm > .input-group-addon,
select.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  line-height: 30px;
}
textarea.input-group-sm > .form-control,
textarea.input-group-sm > .input-group-addon,
textarea.input-group-sm > .input-group-btn > .btn,
select[multiple].input-group-sm > .form-control,
select[multiple].input-group-sm > .input-group-addon,
select[multiple].input-group-sm > .input-group-btn > .btn {
  height: auto;
}
.input-group-addon,
.input-group-btn,
.input-group .form-control {
  display: table-cell;
}
.input-group-addon:not(:first-child):not(:last-child),
.input-group-btn:not(:first-child):not(:last-child),
.input-group .form-control:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.input-group-addon,
.input-group-btn {
  width: 1%;
  white-space: nowrap;
  vertical-align: middle;
}
.input-group-addon {
  padding: 6px 12px;
  font-size: 13px;
  font-weight: normal;
  line-height: 1;
  color: #555555;
  text-align: center;
  background-color: #eeeeee;
  border: 1px solid #ccc;
  border-radius: 2px;
}
.input-group-addon.input-sm {
  padding: 5px 10px;
  font-size: 12px;
  border-radius: 1px;
}
.input-group-addon.input-lg {
  padding: 10px 16px;
  font-size: 17px;
  border-radius: 3px;
}
.input-group-addon input[type="radio"],
.input-group-addon input[type="checkbox"] {
  margin-top: 0;
}
.input-group .form-control:first-child,
.input-group-addon:first-child,
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group > .btn,
.input-group-btn:first-child > .dropdown-toggle,
.input-group-btn:last-child > .btn:not(:last-child):not(.dropdown-toggle),
.input-group-btn:last-child > .btn-group:not(:last-child) > .btn {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.input-group-addon:first-child {
  border-right: 0;
}
.input-group .form-control:last-child,
.input-group-addon:last-child,
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group > .btn,
.input-group-btn:last-child > .dropdown-toggle,
.input-group-btn:first-child > .btn:not(:first-child),
.input-group-btn:first-child > .btn-group:not(:first-child) > .btn {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.input-group-addon:last-child {
  border-left: 0;
}
.input-group-btn {
  position: relative;
  font-size: 0;
  white-space: nowrap;
}
.input-group-btn > .btn {
  position: relative;
}
.input-group-btn > .btn + .btn {
  margin-left: -1px;
}
.input-group-btn > .btn:hover,
.input-group-btn > .btn:focus,
.input-group-btn > .btn:active {
  z-index: 2;
}
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group {
  margin-right: -1px;
}
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group {
  z-index: 2;
  margin-left: -1px;
}
.nav {
  margin-bottom: 0;
  padding-left: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.nav > li.disabled > a {
  color: #777777;
}
.nav > li.disabled > a:hover,
.nav > li.disabled > a:focus {
  color: #777777;
  text-decoration: none;
  background-color: transparent;
  cursor: not-allowed;
}
.nav .open > a,
.nav .open > a:hover,
.nav .open > a:focus {
  background-color: #eeeeee;
  border-color: #337ab7;
}
.nav .nav-divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.nav > li > a > img {
  max-width: none;
}
.nav-tabs {
  border-bottom: 1px solid #ddd;
}
.nav-tabs > li {
  float: left;
  margin-bottom: -1px;
}
.nav-tabs > li > a {
  margin-right: 2px;
  line-height: 1.42857143;
  border: 1px solid transparent;
  border-radius: 2px 2px 0 0;
}
.nav-tabs > li > a:hover {
  border-color: #eeeeee #eeeeee #ddd;
}
.nav-tabs > li.active > a,
.nav-tabs > li.active > a:hover,
.nav-tabs > li.active > a:focus {
  color: #555555;
  background-color: #fff;
  border: 1px solid #ddd;
  border-bottom-color: transparent;
  cursor: default;
}
.nav-tabs.nav-justified {
  width: 100%;
  border-bottom: 0;
}
.nav-tabs.nav-justified > li {
  float: none;
}
.nav-tabs.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-tabs.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-tabs.nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.nav-pills > li {
  float: left;
}
.nav-pills > li > a {
  border-radius: 2px;
}
.nav-pills > li + li {
  margin-left: 2px;
}
.nav-pills > li.active > a,
.nav-pills > li.active > a:hover,
.nav-pills > li.active > a:focus {
  color: #fff;
  background-color: #337ab7;
}
.nav-stacked > li {
  float: none;
}
.nav-stacked > li + li {
  margin-top: 2px;
  margin-left: 0;
}
.nav-justified {
  width: 100%;
}
.nav-justified > li {
  float: none;
}
.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs-justified {
  border-bottom: 0;
}
.nav-tabs-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs-justified > .active > a,
.nav-tabs-justified > .active > a:hover,
.nav-tabs-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs-justified > .active > a,
  .nav-tabs-justified > .active > a:hover,
  .nav-tabs-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.tab-content > .tab-pane {
  display: none;
}
.tab-content > .active {
  display: block;
}
.nav-tabs .dropdown-menu {
  margin-top: -1px;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar {
  position: relative;
  min-height: 30px;
  margin-bottom: 18px;
  border: 1px solid transparent;
}
@media (min-width: 541px) {
  .navbar {
    border-radius: 2px;
  }
}
@media (min-width: 541px) {
  .navbar-header {
    float: left;
  }
}
.navbar-collapse {
  overflow-x: visible;
  padding-right: 0px;
  padding-left: 0px;
  border-top: 1px solid transparent;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
  -webkit-overflow-scrolling: touch;
}
.navbar-collapse.in {
  overflow-y: auto;
}
@media (min-width: 541px) {
  .navbar-collapse {
    width: auto;
    border-top: 0;
    box-shadow: none;
  }
  .navbar-collapse.collapse {
    display: block !important;
    height: auto !important;
    padding-bottom: 0;
    overflow: visible !important;
  }
  .navbar-collapse.in {
    overflow-y: visible;
  }
  .navbar-fixed-top .navbar-collapse,
  .navbar-static-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    padding-left: 0;
    padding-right: 0;
  }
}
.navbar-fixed-top .navbar-collapse,
.navbar-fixed-bottom .navbar-collapse {
  max-height: 340px;
}
@media (max-device-width: 540px) and (orientation: landscape) {
  .navbar-fixed-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    max-height: 200px;
  }
}
.container > .navbar-header,
.container-fluid > .navbar-header,
.container > .navbar-collapse,
.container-fluid > .navbar-collapse {
  margin-right: 0px;
  margin-left: 0px;
}
@media (min-width: 541px) {
  .container > .navbar-header,
  .container-fluid > .navbar-header,
  .container > .navbar-collapse,
  .container-fluid > .navbar-collapse {
    margin-right: 0;
    margin-left: 0;
  }
}
.navbar-static-top {
  z-index: 1000;
  border-width: 0 0 1px;
}
@media (min-width: 541px) {
  .navbar-static-top {
    border-radius: 0;
  }
}
.navbar-fixed-top,
.navbar-fixed-bottom {
  position: fixed;
  right: 0;
  left: 0;
  z-index: 1030;
}
@media (min-width: 541px) {
  .navbar-fixed-top,
  .navbar-fixed-bottom {
    border-radius: 0;
  }
}
.navbar-fixed-top {
  top: 0;
  border-width: 0 0 1px;
}
.navbar-fixed-bottom {
  bottom: 0;
  margin-bottom: 0;
  border-width: 1px 0 0;
}
.navbar-brand {
  float: left;
  padding: 6px 0px;
  font-size: 17px;
  line-height: 18px;
  height: 30px;
}
.navbar-brand:hover,
.navbar-brand:focus {
  text-decoration: none;
}
.navbar-brand > img {
  display: block;
}
@media (min-width: 541px) {
  .navbar > .container .navbar-brand,
  .navbar > .container-fluid .navbar-brand {
    margin-left: 0px;
  }
}
.navbar-toggle {
  position: relative;
  float: right;
  margin-right: 0px;
  padding: 9px 10px;
  margin-top: -2px;
  margin-bottom: -2px;
  background-color: transparent;
  background-image: none;
  border: 1px solid transparent;
  border-radius: 2px;
}
.navbar-toggle:focus {
  outline: 0;
}
.navbar-toggle .icon-bar {
  display: block;
  width: 22px;
  height: 2px;
  border-radius: 1px;
}
.navbar-toggle .icon-bar + .icon-bar {
  margin-top: 4px;
}
@media (min-width: 541px) {
  .navbar-toggle {
    display: none;
  }
}
.navbar-nav {
  margin: 3px 0px;
}
.navbar-nav > li > a {
  padding-top: 10px;
  padding-bottom: 10px;
  line-height: 18px;
}
@media (max-width: 540px) {
  .navbar-nav .open .dropdown-menu {
    position: static;
    float: none;
    width: auto;
    margin-top: 0;
    background-color: transparent;
    border: 0;
    box-shadow: none;
  }
  .navbar-nav .open .dropdown-menu > li > a,
  .navbar-nav .open .dropdown-menu .dropdown-header {
    padding: 5px 15px 5px 25px;
  }
  .navbar-nav .open .dropdown-menu > li > a {
    line-height: 18px;
  }
  .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-nav .open .dropdown-menu > li > a:focus {
    background-image: none;
  }
}
@media (min-width: 541px) {
  .navbar-nav {
    float: left;
    margin: 0;
  }
  .navbar-nav > li {
    float: left;
  }
  .navbar-nav > li > a {
    padding-top: 6px;
    padding-bottom: 6px;
  }
}
.navbar-form {
  margin-left: 0px;
  margin-right: 0px;
  padding: 10px 0px;
  border-top: 1px solid transparent;
  border-bottom: 1px solid transparent;
  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  margin-top: -1px;
  margin-bottom: -1px;
}
@media (min-width: 768px) {
  .navbar-form .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .navbar-form .form-control-static {
    display: inline-block;
  }
  .navbar-form .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .navbar-form .input-group .input-group-addon,
  .navbar-form .input-group .input-group-btn,
  .navbar-form .input-group .form-control {
    width: auto;
  }
  .navbar-form .input-group > .form-control {
    width: 100%;
  }
  .navbar-form .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio,
  .navbar-form .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio label,
  .navbar-form .checkbox label {
    padding-left: 0;
  }
  .navbar-form .radio input[type="radio"],
  .navbar-form .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .navbar-form .has-feedback .form-control-feedback {
    top: 0;
  }
}
@media (max-width: 540px) {
  .navbar-form .form-group {
    margin-bottom: 5px;
  }
  .navbar-form .form-group:last-child {
    margin-bottom: 0;
  }
}
@media (min-width: 541px) {
  .navbar-form {
    width: auto;
    border: 0;
    margin-left: 0;
    margin-right: 0;
    padding-top: 0;
    padding-bottom: 0;
    -webkit-box-shadow: none;
    box-shadow: none;
  }
}
.navbar-nav > li > .dropdown-menu {
  margin-top: 0;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar-fixed-bottom .navbar-nav > li > .dropdown-menu {
  margin-bottom: 0;
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.navbar-btn {
  margin-top: -1px;
  margin-bottom: -1px;
}
.navbar-btn.btn-sm {
  margin-top: 0px;
  margin-bottom: 0px;
}
.navbar-btn.btn-xs {
  margin-top: 4px;
  margin-bottom: 4px;
}
.navbar-text {
  margin-top: 6px;
  margin-bottom: 6px;
}
@media (min-width: 541px) {
  .navbar-text {
    float: left;
    margin-left: 0px;
    margin-right: 0px;
  }
}
@media (min-width: 541px) {
  .navbar-left {
    float: left !important;
    float: left;
  }
  .navbar-right {
    float: right !important;
    float: right;
    margin-right: 0px;
  }
  .navbar-right ~ .navbar-right {
    margin-right: 0;
  }
}
.navbar-default {
  background-color: #f8f8f8;
  border-color: #e7e7e7;
}
.navbar-default .navbar-brand {
  color: #777;
}
.navbar-default .navbar-brand:hover,
.navbar-default .navbar-brand:focus {
  color: #5e5e5e;
  background-color: transparent;
}
.navbar-default .navbar-text {
  color: #777;
}
.navbar-default .navbar-nav > li > a {
  color: #777;
}
.navbar-default .navbar-nav > li > a:hover,
.navbar-default .navbar-nav > li > a:focus {
  color: #333;
  background-color: transparent;
}
.navbar-default .navbar-nav > .active > a,
.navbar-default .navbar-nav > .active > a:hover,
.navbar-default .navbar-nav > .active > a:focus {
  color: #555;
  background-color: #e7e7e7;
}
.navbar-default .navbar-nav > .disabled > a,
.navbar-default .navbar-nav > .disabled > a:hover,
.navbar-default .navbar-nav > .disabled > a:focus {
  color: #ccc;
  background-color: transparent;
}
.navbar-default .navbar-toggle {
  border-color: #ddd;
}
.navbar-default .navbar-toggle:hover,
.navbar-default .navbar-toggle:focus {
  background-color: #ddd;
}
.navbar-default .navbar-toggle .icon-bar {
  background-color: #888;
}
.navbar-default .navbar-collapse,
.navbar-default .navbar-form {
  border-color: #e7e7e7;
}
.navbar-default .navbar-nav > .open > a,
.navbar-default .navbar-nav > .open > a:hover,
.navbar-default .navbar-nav > .open > a:focus {
  background-color: #e7e7e7;
  color: #555;
}
@media (max-width: 540px) {
  .navbar-default .navbar-nav .open .dropdown-menu > li > a {
    color: #777;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #333;
    background-color: transparent;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #555;
    background-color: #e7e7e7;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #ccc;
    background-color: transparent;
  }
}
.navbar-default .navbar-link {
  color: #777;
}
.navbar-default .navbar-link:hover {
  color: #333;
}
.navbar-default .btn-link {
  color: #777;
}
.navbar-default .btn-link:hover,
.navbar-default .btn-link:focus {
  color: #333;
}
.navbar-default .btn-link[disabled]:hover,
fieldset[disabled] .navbar-default .btn-link:hover,
.navbar-default .btn-link[disabled]:focus,
fieldset[disabled] .navbar-default .btn-link:focus {
  color: #ccc;
}
.navbar-inverse {
  background-color: #222;
  border-color: #080808;
}
.navbar-inverse .navbar-brand {
  color: #9d9d9d;
}
.navbar-inverse .navbar-brand:hover,
.navbar-inverse .navbar-brand:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-text {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a:hover,
.navbar-inverse .navbar-nav > li > a:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-nav > .active > a,
.navbar-inverse .navbar-nav > .active > a:hover,
.navbar-inverse .navbar-nav > .active > a:focus {
  color: #fff;
  background-color: #080808;
}
.navbar-inverse .navbar-nav > .disabled > a,
.navbar-inverse .navbar-nav > .disabled > a:hover,
.navbar-inverse .navbar-nav > .disabled > a:focus {
  color: #444;
  background-color: transparent;
}
.navbar-inverse .navbar-toggle {
  border-color: #333;
}
.navbar-inverse .navbar-toggle:hover,
.navbar-inverse .navbar-toggle:focus {
  background-color: #333;
}
.navbar-inverse .navbar-toggle .icon-bar {
  background-color: #fff;
}
.navbar-inverse .navbar-collapse,
.navbar-inverse .navbar-form {
  border-color: #101010;
}
.navbar-inverse .navbar-nav > .open > a,
.navbar-inverse .navbar-nav > .open > a:hover,
.navbar-inverse .navbar-nav > .open > a:focus {
  background-color: #080808;
  color: #fff;
}
@media (max-width: 540px) {
  .navbar-inverse .navbar-nav .open .dropdown-menu > .dropdown-header {
    border-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu .divider {
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a {
    color: #9d9d9d;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #fff;
    background-color: transparent;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #fff;
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #444;
    background-color: transparent;
  }
}
.navbar-inverse .navbar-link {
  color: #9d9d9d;
}
.navbar-inverse .navbar-link:hover {
  color: #fff;
}
.navbar-inverse .btn-link {
  color: #9d9d9d;
}
.navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link:focus {
  color: #fff;
}
.navbar-inverse .btn-link[disabled]:hover,
fieldset[disabled] .navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link[disabled]:focus,
fieldset[disabled] .navbar-inverse .btn-link:focus {
  color: #444;
}
.breadcrumb {
  padding: 8px 15px;
  margin-bottom: 18px;
  list-style: none;
  background-color: #f5f5f5;
  border-radius: 2px;
}
.breadcrumb > li {
  display: inline-block;
}
.breadcrumb > li + li:before {
  content: "/\00a0";
  padding: 0 5px;
  color: #5e5e5e;
}
.breadcrumb > .active {
  color: #777777;
}
.pagination {
  display: inline-block;
  padding-left: 0;
  margin: 18px 0;
  border-radius: 2px;
}
.pagination > li {
  display: inline;
}
.pagination > li > a,
.pagination > li > span {
  position: relative;
  float: left;
  padding: 6px 12px;
  line-height: 1.42857143;
  text-decoration: none;
  color: #337ab7;
  background-color: #fff;
  border: 1px solid #ddd;
  margin-left: -1px;
}
.pagination > li:first-child > a,
.pagination > li:first-child > span {
  margin-left: 0;
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.pagination > li:last-child > a,
.pagination > li:last-child > span {
  border-bottom-right-radius: 2px;
  border-top-right-radius: 2px;
}
.pagination > li > a:hover,
.pagination > li > span:hover,
.pagination > li > a:focus,
.pagination > li > span:focus {
  z-index: 2;
  color: #23527c;
  background-color: #eeeeee;
  border-color: #ddd;
}
.pagination > .active > a,
.pagination > .active > span,
.pagination > .active > a:hover,
.pagination > .active > span:hover,
.pagination > .active > a:focus,
.pagination > .active > span:focus {
  z-index: 3;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
  cursor: default;
}
.pagination > .disabled > span,
.pagination > .disabled > span:hover,
.pagination > .disabled > span:focus,
.pagination > .disabled > a,
.pagination > .disabled > a:hover,
.pagination > .disabled > a:focus {
  color: #777777;
  background-color: #fff;
  border-color: #ddd;
  cursor: not-allowed;
}
.pagination-lg > li > a,
.pagination-lg > li > span {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.pagination-lg > li:first-child > a,
.pagination-lg > li:first-child > span {
  border-bottom-left-radius: 3px;
  border-top-left-radius: 3px;
}
.pagination-lg > li:last-child > a,
.pagination-lg > li:last-child > span {
  border-bottom-right-radius: 3px;
  border-top-right-radius: 3px;
}
.pagination-sm > li > a,
.pagination-sm > li > span {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.pagination-sm > li:first-child > a,
.pagination-sm > li:first-child > span {
  border-bottom-left-radius: 1px;
  border-top-left-radius: 1px;
}
.pagination-sm > li:last-child > a,
.pagination-sm > li:last-child > span {
  border-bottom-right-radius: 1px;
  border-top-right-radius: 1px;
}
.pager {
  padding-left: 0;
  margin: 18px 0;
  list-style: none;
  text-align: center;
}
.pager li {
  display: inline;
}
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 5px 14px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 15px;
}
.pager li > a:hover,
.pager li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.pager .next > a,
.pager .next > span {
  float: right;
}
.pager .previous > a,
.pager .previous > span {
  float: left;
}
.pager .disabled > a,
.pager .disabled > a:hover,
.pager .disabled > a:focus,
.pager .disabled > span {
  color: #777777;
  background-color: #fff;
  cursor: not-allowed;
}
.label {
  display: inline;
  padding: .2em .6em .3em;
  font-size: 75%;
  font-weight: bold;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: baseline;
  border-radius: .25em;
}
a.label:hover,
a.label:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.label:empty {
  display: none;
}
.btn .label {
  position: relative;
  top: -1px;
}
.label-default {
  background-color: #777777;
}
.label-default[href]:hover,
.label-default[href]:focus {
  background-color: #5e5e5e;
}
.label-primary {
  background-color: #337ab7;
}
.label-primary[href]:hover,
.label-primary[href]:focus {
  background-color: #286090;
}
.label-success {
  background-color: #5cb85c;
}
.label-success[href]:hover,
.label-success[href]:focus {
  background-color: #449d44;
}
.label-info {
  background-color: #5bc0de;
}
.label-info[href]:hover,
.label-info[href]:focus {
  background-color: #31b0d5;
}
.label-warning {
  background-color: #f0ad4e;
}
.label-warning[href]:hover,
.label-warning[href]:focus {
  background-color: #ec971f;
}
.label-danger {
  background-color: #d9534f;
}
.label-danger[href]:hover,
.label-danger[href]:focus {
  background-color: #c9302c;
}
.badge {
  display: inline-block;
  min-width: 10px;
  padding: 3px 7px;
  font-size: 12px;
  font-weight: bold;
  color: #fff;
  line-height: 1;
  vertical-align: middle;
  white-space: nowrap;
  text-align: center;
  background-color: #777777;
  border-radius: 10px;
}
.badge:empty {
  display: none;
}
.btn .badge {
  position: relative;
  top: -1px;
}
.btn-xs .badge,
.btn-group-xs > .btn .badge {
  top: 0;
  padding: 1px 5px;
}
a.badge:hover,
a.badge:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.list-group-item.active > .badge,
.nav-pills > .active > a > .badge {
  color: #337ab7;
  background-color: #fff;
}
.list-group-item > .badge {
  float: right;
}
.list-group-item > .badge + .badge {
  margin-right: 5px;
}
.nav-pills > li > a > .badge {
  margin-left: 3px;
}
.jumbotron {
  padding-top: 30px;
  padding-bottom: 30px;
  margin-bottom: 30px;
  color: inherit;
  background-color: #eeeeee;
}
.jumbotron h1,
.jumbotron .h1 {
  color: inherit;
}
.jumbotron p {
  margin-bottom: 15px;
  font-size: 20px;
  font-weight: 200;
}
.jumbotron > hr {
  border-top-color: #d5d5d5;
}
.container .jumbotron,
.container-fluid .jumbotron {
  border-radius: 3px;
  padding-left: 0px;
  padding-right: 0px;
}
.jumbotron .container {
  max-width: 100%;
}
@media screen and (min-width: 768px) {
  .jumbotron {
    padding-top: 48px;
    padding-bottom: 48px;
  }
  .container .jumbotron,
  .container-fluid .jumbotron {
    padding-left: 60px;
    padding-right: 60px;
  }
  .jumbotron h1,
  .jumbotron .h1 {
    font-size: 59px;
  }
}
.thumbnail {
  display: block;
  padding: 4px;
  margin-bottom: 18px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: border 0.2s ease-in-out;
  -o-transition: border 0.2s ease-in-out;
  transition: border 0.2s ease-in-out;
}
.thumbnail > img,
.thumbnail a > img {
  margin-left: auto;
  margin-right: auto;
}
a.thumbnail:hover,
a.thumbnail:focus,
a.thumbnail.active {
  border-color: #337ab7;
}
.thumbnail .caption {
  padding: 9px;
  color: #000;
}
.alert {
  padding: 15px;
  margin-bottom: 18px;
  border: 1px solid transparent;
  border-radius: 2px;
}
.alert h4 {
  margin-top: 0;
  color: inherit;
}
.alert .alert-link {
  font-weight: bold;
}
.alert > p,
.alert > ul {
  margin-bottom: 0;
}
.alert > p + p {
  margin-top: 5px;
}
.alert-dismissable,
.alert-dismissible {
  padding-right: 35px;
}
.alert-dismissable .close,
.alert-dismissible .close {
  position: relative;
  top: -2px;
  right: -21px;
  color: inherit;
}
.alert-success {
  background-color: #dff0d8;
  border-color: #d6e9c6;
  color: #3c763d;
}
.alert-success hr {
  border-top-color: #c9e2b3;
}
.alert-success .alert-link {
  color: #2b542c;
}
.alert-info {
  background-color: #d9edf7;
  border-color: #bce8f1;
  color: #31708f;
}
.alert-info hr {
  border-top-color: #a6e1ec;
}
.alert-info .alert-link {
  color: #245269;
}
.alert-warning {
  background-color: #fcf8e3;
  border-color: #faebcc;
  color: #8a6d3b;
}
.alert-warning hr {
  border-top-color: #f7e1b5;
}
.alert-warning .alert-link {
  color: #66512c;
}
.alert-danger {
  background-color: #f2dede;
  border-color: #ebccd1;
  color: #a94442;
}
.alert-danger hr {
  border-top-color: #e4b9c0;
}
.alert-danger .alert-link {
  color: #843534;
}
@-webkit-keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
@keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
.progress {
  overflow: hidden;
  height: 18px;
  margin-bottom: 18px;
  background-color: #f5f5f5;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
}
.progress-bar {
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 18px;
  color: #fff;
  text-align: center;
  background-color: #337ab7;
  -webkit-box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  -webkit-transition: width 0.6s ease;
  -o-transition: width 0.6s ease;
  transition: width 0.6s ease;
}
.progress-striped .progress-bar,
.progress-bar-striped {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-size: 40px 40px;
}
.progress.active .progress-bar,
.progress-bar.active {
  -webkit-animation: progress-bar-stripes 2s linear infinite;
  -o-animation: progress-bar-stripes 2s linear infinite;
  animation: progress-bar-stripes 2s linear infinite;
}
.progress-bar-success {
  background-color: #5cb85c;
}
.progress-striped .progress-bar-success {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-info {
  background-color: #5bc0de;
}
.progress-striped .progress-bar-info {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-warning {
  background-color: #f0ad4e;
}
.progress-striped .progress-bar-warning {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-danger {
  background-color: #d9534f;
}
.progress-striped .progress-bar-danger {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.media {
  margin-top: 15px;
}
.media:first-child {
  margin-top: 0;
}
.media,
.media-body {
  zoom: 1;
  overflow: hidden;
}
.media-body {
  width: 10000px;
}
.media-object {
  display: block;
}
.media-object.img-thumbnail {
  max-width: none;
}
.media-right,
.media > .pull-right {
  padding-left: 10px;
}
.media-left,
.media > .pull-left {
  padding-right: 10px;
}
.media-left,
.media-right,
.media-body {
  display: table-cell;
  vertical-align: top;
}
.media-middle {
  vertical-align: middle;
}
.media-bottom {
  vertical-align: bottom;
}
.media-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.media-list {
  padding-left: 0;
  list-style: none;
}
.list-group {
  margin-bottom: 20px;
  padding-left: 0;
}
.list-group-item {
  position: relative;
  display: block;
  padding: 10px 15px;
  margin-bottom: -1px;
  background-color: #fff;
  border: 1px solid #ddd;
}
.list-group-item:first-child {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
}
.list-group-item:last-child {
  margin-bottom: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
a.list-group-item,
button.list-group-item {
  color: #555;
}
a.list-group-item .list-group-item-heading,
button.list-group-item .list-group-item-heading {
  color: #333;
}
a.list-group-item:hover,
button.list-group-item:hover,
a.list-group-item:focus,
button.list-group-item:focus {
  text-decoration: none;
  color: #555;
  background-color: #f5f5f5;
}
button.list-group-item {
  width: 100%;
  text-align: left;
}
.list-group-item.disabled,
.list-group-item.disabled:hover,
.list-group-item.disabled:focus {
  background-color: #eeeeee;
  color: #777777;
  cursor: not-allowed;
}
.list-group-item.disabled .list-group-item-heading,
.list-group-item.disabled:hover .list-group-item-heading,
.list-group-item.disabled:focus .list-group-item-heading {
  color: inherit;
}
.list-group-item.disabled .list-group-item-text,
.list-group-item.disabled:hover .list-group-item-text,
.list-group-item.disabled:focus .list-group-item-text {
  color: #777777;
}
.list-group-item.active,
.list-group-item.active:hover,
.list-group-item.active:focus {
  z-index: 2;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.list-group-item.active .list-group-item-heading,
.list-group-item.active:hover .list-group-item-heading,
.list-group-item.active:focus .list-group-item-heading,
.list-group-item.active .list-group-item-heading > small,
.list-group-item.active:hover .list-group-item-heading > small,
.list-group-item.active:focus .list-group-item-heading > small,
.list-group-item.active .list-group-item-heading > .small,
.list-group-item.active:hover .list-group-item-heading > .small,
.list-group-item.active:focus .list-group-item-heading > .small {
  color: inherit;
}
.list-group-item.active .list-group-item-text,
.list-group-item.active:hover .list-group-item-text,
.list-group-item.active:focus .list-group-item-text {
  color: #c7ddef;
}
.list-group-item-success {
  color: #3c763d;
  background-color: #dff0d8;
}
a.list-group-item-success,
button.list-group-item-success {
  color: #3c763d;
}
a.list-group-item-success .list-group-item-heading,
button.list-group-item-success .list-group-item-heading {
  color: inherit;
}
a.list-group-item-success:hover,
button.list-group-item-success:hover,
a.list-group-item-success:focus,
button.list-group-item-success:focus {
  color: #3c763d;
  background-color: #d0e9c6;
}
a.list-group-item-success.active,
button.list-group-item-success.active,
a.list-group-item-success.active:hover,
button.list-group-item-success.active:hover,
a.list-group-item-success.active:focus,
button.list-group-item-success.active:focus {
  color: #fff;
  background-color: #3c763d;
  border-color: #3c763d;
}
.list-group-item-info {
  color: #31708f;
  background-color: #d9edf7;
}
a.list-group-item-info,
button.list-group-item-info {
  color: #31708f;
}
a.list-group-item-info .list-group-item-heading,
button.list-group-item-info .list-group-item-heading {
  color: inherit;
}
a.list-group-item-info:hover,
button.list-group-item-info:hover,
a.list-group-item-info:focus,
button.list-group-item-info:focus {
  color: #31708f;
  background-color: #c4e3f3;
}
a.list-group-item-info.active,
button.list-group-item-info.active,
a.list-group-item-info.active:hover,
button.list-group-item-info.active:hover,
a.list-group-item-info.active:focus,
button.list-group-item-info.active:focus {
  color: #fff;
  background-color: #31708f;
  border-color: #31708f;
}
.list-group-item-warning {
  color: #8a6d3b;
  background-color: #fcf8e3;
}
a.list-group-item-warning,
button.list-group-item-warning {
  color: #8a6d3b;
}
a.list-group-item-warning .list-group-item-heading,
button.list-group-item-warning .list-group-item-heading {
  color: inherit;
}
a.list-group-item-warning:hover,
button.list-group-item-warning:hover,
a.list-group-item-warning:focus,
button.list-group-item-warning:focus {
  color: #8a6d3b;
  background-color: #faf2cc;
}
a.list-group-item-warning.active,
button.list-group-item-warning.active,
a.list-group-item-warning.active:hover,
button.list-group-item-warning.active:hover,
a.list-group-item-warning.active:focus,
button.list-group-item-warning.active:focus {
  color: #fff;
  background-color: #8a6d3b;
  border-color: #8a6d3b;
}
.list-group-item-danger {
  color: #a94442;
  background-color: #f2dede;
}
a.list-group-item-danger,
button.list-group-item-danger {
  color: #a94442;
}
a.list-group-item-danger .list-group-item-heading,
button.list-group-item-danger .list-group-item-heading {
  color: inherit;
}
a.list-group-item-danger:hover,
button.list-group-item-danger:hover,
a.list-group-item-danger:focus,
button.list-group-item-danger:focus {
  color: #a94442;
  background-color: #ebcccc;
}
a.list-group-item-danger.active,
button.list-group-item-danger.active,
a.list-group-item-danger.active:hover,
button.list-group-item-danger.active:hover,
a.list-group-item-danger.active:focus,
button.list-group-item-danger.active:focus {
  color: #fff;
  background-color: #a94442;
  border-color: #a94442;
}
.list-group-item-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.list-group-item-text {
  margin-bottom: 0;
  line-height: 1.3;
}
.panel {
  margin-bottom: 18px;
  background-color: #fff;
  border: 1px solid transparent;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
}
.panel-body {
  padding: 15px;
}
.panel-heading {
  padding: 10px 15px;
  border-bottom: 1px solid transparent;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel-heading > .dropdown .dropdown-toggle {
  color: inherit;
}
.panel-title {
  margin-top: 0;
  margin-bottom: 0;
  font-size: 15px;
  color: inherit;
}
.panel-title > a,
.panel-title > small,
.panel-title > .small,
.panel-title > small > a,
.panel-title > .small > a {
  color: inherit;
}
.panel-footer {
  padding: 10px 15px;
  background-color: #f5f5f5;
  border-top: 1px solid #ddd;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .list-group,
.panel > .panel-collapse > .list-group {
  margin-bottom: 0;
}
.panel > .list-group .list-group-item,
.panel > .panel-collapse > .list-group .list-group-item {
  border-width: 1px 0;
  border-radius: 0;
}
.panel > .list-group:first-child .list-group-item:first-child,
.panel > .panel-collapse > .list-group:first-child .list-group-item:first-child {
  border-top: 0;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .list-group:last-child .list-group-item:last-child,
.panel > .panel-collapse > .list-group:last-child .list-group-item:last-child {
  border-bottom: 0;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .panel-heading + .panel-collapse > .list-group .list-group-item:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.panel-heading + .list-group .list-group-item:first-child {
  border-top-width: 0;
}
.list-group + .panel-footer {
  border-top-width: 0;
}
.panel > .table,
.panel > .table-responsive > .table,
.panel > .panel-collapse > .table {
  margin-bottom: 0;
}
.panel > .table caption,
.panel > .table-responsive > .table caption,
.panel > .panel-collapse > .table caption {
  padding-left: 15px;
  padding-right: 15px;
}
.panel > .table:first-child,
.panel > .table-responsive:first-child > .table:first-child {
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child {
  border-top-left-radius: 1px;
  border-top-right-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:first-child {
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:last-child {
  border-top-right-radius: 1px;
}
.panel > .table:last-child,
.panel > .table-responsive:last-child > .table:last-child {
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child {
  border-bottom-left-radius: 1px;
  border-bottom-right-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:first-child {
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:last-child {
  border-bottom-right-radius: 1px;
}
.panel > .panel-body + .table,
.panel > .panel-body + .table-responsive,
.panel > .table + .panel-body,
.panel > .table-responsive + .panel-body {
  border-top: 1px solid #ddd;
}
.panel > .table > tbody:first-child > tr:first-child th,
.panel > .table > tbody:first-child > tr:first-child td {
  border-top: 0;
}
.panel > .table-bordered,
.panel > .table-responsive > .table-bordered {
  border: 0;
}
.panel > .table-bordered > thead > tr > th:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:first-child,
.panel > .table-bordered > tbody > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:first-child,
.panel > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-bordered > thead > tr > td:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:first-child,
.panel > .table-bordered > tbody > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:first-child,
.panel > .table-bordered > tfoot > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:first-child {
  border-left: 0;
}
.panel > .table-bordered > thead > tr > th:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:last-child,
.panel > .table-bordered > tbody > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:last-child,
.panel > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-bordered > thead > tr > td:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:last-child,
.panel > .table-bordered > tbody > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:last-child,
.panel > .table-bordered > tfoot > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:last-child {
  border-right: 0;
}
.panel > .table-bordered > thead > tr:first-child > td,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > td,
.panel > .table-bordered > tbody > tr:first-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > td,
.panel > .table-bordered > thead > tr:first-child > th,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > th,
.panel > .table-bordered > tbody > tr:first-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > th {
  border-bottom: 0;
}
.panel > .table-bordered > tbody > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > td,
.panel > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-bordered > tbody > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > th,
.panel > .table-bordered > tfoot > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > th {
  border-bottom: 0;
}
.panel > .table-responsive {
  border: 0;
  margin-bottom: 0;
}
.panel-group {
  margin-bottom: 18px;
}
.panel-group .panel {
  margin-bottom: 0;
  border-radius: 2px;
}
.panel-group .panel + .panel {
  margin-top: 5px;
}
.panel-group .panel-heading {
  border-bottom: 0;
}
.panel-group .panel-heading + .panel-collapse > .panel-body,
.panel-group .panel-heading + .panel-collapse > .list-group {
  border-top: 1px solid #ddd;
}
.panel-group .panel-footer {
  border-top: 0;
}
.panel-group .panel-footer + .panel-collapse .panel-body {
  border-bottom: 1px solid #ddd;
}
.panel-default {
  border-color: #ddd;
}
.panel-default > .panel-heading {
  color: #333333;
  background-color: #f5f5f5;
  border-color: #ddd;
}
.panel-default > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ddd;
}
.panel-default > .panel-heading .badge {
  color: #f5f5f5;
  background-color: #333333;
}
.panel-default > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ddd;
}
.panel-primary {
  border-color: #337ab7;
}
.panel-primary > .panel-heading {
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.panel-primary > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #337ab7;
}
.panel-primary > .panel-heading .badge {
  color: #337ab7;
  background-color: #fff;
}
.panel-primary > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #337ab7;
}
.panel-success {
  border-color: #d6e9c6;
}
.panel-success > .panel-heading {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #d6e9c6;
}
.panel-success > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #d6e9c6;
}
.panel-success > .panel-heading .badge {
  color: #dff0d8;
  background-color: #3c763d;
}
.panel-success > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #d6e9c6;
}
.panel-info {
  border-color: #bce8f1;
}
.panel-info > .panel-heading {
  color: #31708f;
  background-color: #d9edf7;
  border-color: #bce8f1;
}
.panel-info > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #bce8f1;
}
.panel-info > .panel-heading .badge {
  color: #d9edf7;
  background-color: #31708f;
}
.panel-info > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #bce8f1;
}
.panel-warning {
  border-color: #faebcc;
}
.panel-warning > .panel-heading {
  color: #8a6d3b;
  background-color: #fcf8e3;
  border-color: #faebcc;
}
.panel-warning > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #faebcc;
}
.panel-warning > .panel-heading .badge {
  color: #fcf8e3;
  background-color: #8a6d3b;
}
.panel-warning > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #faebcc;
}
.panel-danger {
  border-color: #ebccd1;
}
.panel-danger > .panel-heading {
  color: #a94442;
  background-color: #f2dede;
  border-color: #ebccd1;
}
.panel-danger > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ebccd1;
}
.panel-danger > .panel-heading .badge {
  color: #f2dede;
  background-color: #a94442;
}
.panel-danger > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ebccd1;
}
.embed-responsive {
  position: relative;
  display: block;
  height: 0;
  padding: 0;
  overflow: hidden;
}
.embed-responsive .embed-responsive-item,
.embed-responsive iframe,
.embed-responsive embed,
.embed-responsive object,
.embed-responsive video {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  height: 100%;
  width: 100%;
  border: 0;
}
.embed-responsive-16by9 {
  padding-bottom: 56.25%;
}
.embed-responsive-4by3 {
  padding-bottom: 75%;
}
.well {
  min-height: 20px;
  padding: 19px;
  margin-bottom: 20px;
  background-color: #f5f5f5;
  border: 1px solid #e3e3e3;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
}
.well blockquote {
  border-color: #ddd;
  border-color: rgba(0, 0, 0, 0.15);
}
.well-lg {
  padding: 24px;
  border-radius: 3px;
}
.well-sm {
  padding: 9px;
  border-radius: 1px;
}
.close {
  float: right;
  font-size: 19.5px;
  font-weight: bold;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  opacity: 0.2;
  filter: alpha(opacity=20);
}
.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
  opacity: 0.5;
  filter: alpha(opacity=50);
}
button.close {
  padding: 0;
  cursor: pointer;
  background: transparent;
  border: 0;
  -webkit-appearance: none;
}
.modal-open {
  overflow: hidden;
}
.modal {
  display: none;
  overflow: hidden;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1050;
  -webkit-overflow-scrolling: touch;
  outline: 0;
}
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, -25%);
  -ms-transform: translate(0, -25%);
  -o-transform: translate(0, -25%);
  transform: translate(0, -25%);
  -webkit-transition: -webkit-transform 0.3s ease-out;
  -moz-transition: -moz-transform 0.3s ease-out;
  -o-transition: -o-transform 0.3s ease-out;
  transition: transform 0.3s ease-out;
}
.modal.in .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
.modal-open .modal {
  overflow-x: hidden;
  overflow-y: auto;
}
.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}
.modal-content {
  position: relative;
  background-color: #fff;
  border: 1px solid #999;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  background-clip: padding-box;
  outline: 0;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #000;
}
.modal-backdrop.fade {
  opacity: 0;
  filter: alpha(opacity=0);
}
.modal-backdrop.in {
  opacity: 0.5;
  filter: alpha(opacity=50);
}
.modal-header {
  padding: 15px;
  border-bottom: 1px solid #e5e5e5;
}
.modal-header .close {
  margin-top: -2px;
}
.modal-title {
  margin: 0;
  line-height: 1.42857143;
}
.modal-body {
  position: relative;
  padding: 15px;
}
.modal-footer {
  padding: 15px;
  text-align: right;
  border-top: 1px solid #e5e5e5;
}
.modal-footer .btn + .btn {
  margin-left: 5px;
  margin-bottom: 0;
}
.modal-footer .btn-group .btn + .btn {
  margin-left: -1px;
}
.modal-footer .btn-block + .btn-block {
  margin-left: 0;
}
.modal-scrollbar-measure {
  position: absolute;
  top: -9999px;
  width: 50px;
  height: 50px;
  overflow: scroll;
}
@media (min-width: 768px) {
  .modal-dialog {
    width: 600px;
    margin: 30px auto;
  }
  .modal-content {
    -webkit-box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  }
  .modal-sm {
    width: 300px;
  }
}
@media (min-width: 992px) {
  .modal-lg {
    width: 900px;
  }
}
.tooltip {
  position: absolute;
  z-index: 1070;
  display: block;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 12px;
  opacity: 0;
  filter: alpha(opacity=0);
}
.tooltip.in {
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.tooltip.top {
  margin-top: -3px;
  padding: 5px 0;
}
.tooltip.right {
  margin-left: 3px;
  padding: 0 5px;
}
.tooltip.bottom {
  margin-top: 3px;
  padding: 5px 0;
}
.tooltip.left {
  margin-left: -3px;
  padding: 0 5px;
}
.tooltip-inner {
  max-width: 200px;
  padding: 3px 8px;
  color: #fff;
  text-align: center;
  background-color: #000;
  border-radius: 2px;
}
.tooltip-arrow {
  position: absolute;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.tooltip.top .tooltip-arrow {
  bottom: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-left .tooltip-arrow {
  bottom: 0;
  right: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-right .tooltip-arrow {
  bottom: 0;
  left: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.right .tooltip-arrow {
  top: 50%;
  left: 0;
  margin-top: -5px;
  border-width: 5px 5px 5px 0;
  border-right-color: #000;
}
.tooltip.left .tooltip-arrow {
  top: 50%;
  right: 0;
  margin-top: -5px;
  border-width: 5px 0 5px 5px;
  border-left-color: #000;
}
.tooltip.bottom .tooltip-arrow {
  top: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-left .tooltip-arrow {
  top: 0;
  right: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-right .tooltip-arrow {
  top: 0;
  left: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.popover {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1060;
  display: none;
  max-width: 276px;
  padding: 1px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 13px;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}
.popover.top {
  margin-top: -10px;
}
.popover.right {
  margin-left: 10px;
}
.popover.bottom {
  margin-top: 10px;
}
.popover.left {
  margin-left: -10px;
}
.popover-title {
  margin: 0;
  padding: 8px 14px;
  font-size: 13px;
  background-color: #f7f7f7;
  border-bottom: 1px solid #ebebeb;
  border-radius: 2px 2px 0 0;
}
.popover-content {
  padding: 9px 14px;
}
.popover > .arrow,
.popover > .arrow:after {
  position: absolute;
  display: block;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.popover > .arrow {
  border-width: 11px;
}
.popover > .arrow:after {
  border-width: 10px;
  content: "";
}
.popover.top > .arrow {
  left: 50%;
  margin-left: -11px;
  border-bottom-width: 0;
  border-top-color: #999999;
  border-top-color: rgba(0, 0, 0, 0.25);
  bottom: -11px;
}
.popover.top > .arrow:after {
  content: " ";
  bottom: 1px;
  margin-left: -10px;
  border-bottom-width: 0;
  border-top-color: #fff;
}
.popover.right > .arrow {
  top: 50%;
  left: -11px;
  margin-top: -11px;
  border-left-width: 0;
  border-right-color: #999999;
  border-right-color: rgba(0, 0, 0, 0.25);
}
.popover.right > .arrow:after {
  content: " ";
  left: 1px;
  bottom: -10px;
  border-left-width: 0;
  border-right-color: #fff;
}
.popover.bottom > .arrow {
  left: 50%;
  margin-left: -11px;
  border-top-width: 0;
  border-bottom-color: #999999;
  border-bottom-color: rgba(0, 0, 0, 0.25);
  top: -11px;
}
.popover.bottom > .arrow:after {
  content: " ";
  top: 1px;
  margin-left: -10px;
  border-top-width: 0;
  border-bottom-color: #fff;
}
.popover.left > .arrow {
  top: 50%;
  right: -11px;
  margin-top: -11px;
  border-right-width: 0;
  border-left-color: #999999;
  border-left-color: rgba(0, 0, 0, 0.25);
}
.popover.left > .arrow:after {
  content: " ";
  right: 1px;
  border-right-width: 0;
  border-left-color: #fff;
  bottom: -10px;
}
.carousel {
  position: relative;
}
.carousel-inner {
  position: relative;
  overflow: hidden;
  width: 100%;
}
.carousel-inner > .item {
  display: none;
  position: relative;
  -webkit-transition: 0.6s ease-in-out left;
  -o-transition: 0.6s ease-in-out left;
  transition: 0.6s ease-in-out left;
}
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  line-height: 1;
}
@media all and (transform-3d), (-webkit-transform-3d) {
  .carousel-inner > .item {
    -webkit-transition: -webkit-transform 0.6s ease-in-out;
    -moz-transition: -moz-transform 0.6s ease-in-out;
    -o-transition: -o-transform 0.6s ease-in-out;
    transition: transform 0.6s ease-in-out;
    -webkit-backface-visibility: hidden;
    -moz-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-perspective: 1000px;
    -moz-perspective: 1000px;
    perspective: 1000px;
  }
  .carousel-inner > .item.next,
  .carousel-inner > .item.active.right {
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.prev,
  .carousel-inner > .item.active.left {
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.next.left,
  .carousel-inner > .item.prev.right,
  .carousel-inner > .item.active {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
    left: 0;
  }
}
.carousel-inner > .active,
.carousel-inner > .next,
.carousel-inner > .prev {
  display: block;
}
.carousel-inner > .active {
  left: 0;
}
.carousel-inner > .next,
.carousel-inner > .prev {
  position: absolute;
  top: 0;
  width: 100%;
}
.carousel-inner > .next {
  left: 100%;
}
.carousel-inner > .prev {
  left: -100%;
}
.carousel-inner > .next.left,
.carousel-inner > .prev.right {
  left: 0;
}
.carousel-inner > .active.left {
  left: -100%;
}
.carousel-inner > .active.right {
  left: 100%;
}
.carousel-control {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  width: 15%;
  opacity: 0.5;
  filter: alpha(opacity=50);
  font-size: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
  background-color: rgba(0, 0, 0, 0);
}
.carousel-control.left {
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#80000000', endColorstr='#00000000', GradientType=1);
}
.carousel-control.right {
  left: auto;
  right: 0;
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#00000000', endColorstr='#80000000', GradientType=1);
}
.carousel-control:hover,
.carousel-control:focus {
  outline: 0;
  color: #fff;
  text-decoration: none;
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.carousel-control .icon-prev,
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-left,
.carousel-control .glyphicon-chevron-right {
  position: absolute;
  top: 50%;
  margin-top: -10px;
  z-index: 5;
  display: inline-block;
}
.carousel-control .icon-prev,
.carousel-control .glyphicon-chevron-left {
  left: 50%;
  margin-left: -10px;
}
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-right {
  right: 50%;
  margin-right: -10px;
}
.carousel-control .icon-prev,
.carousel-control .icon-next {
  width: 20px;
  height: 20px;
  line-height: 1;
  font-family: serif;
}
.carousel-control .icon-prev:before {
  content: '\2039';
}
.carousel-control .icon-next:before {
  content: '\203a';
}
.carousel-indicators {
  position: absolute;
  bottom: 10px;
  left: 50%;
  z-index: 15;
  width: 60%;
  margin-left: -30%;
  padding-left: 0;
  list-style: none;
  text-align: center;
}
.carousel-indicators li {
  display: inline-block;
  width: 10px;
  height: 10px;
  margin: 1px;
  text-indent: -999px;
  border: 1px solid #fff;
  border-radius: 10px;
  cursor: pointer;
  background-color: #000 \9;
  background-color: rgba(0, 0, 0, 0);
}
.carousel-indicators .active {
  margin: 0;
  width: 12px;
  height: 12px;
  background-color: #fff;
}
.carousel-caption {
  position: absolute;
  left: 15%;
  right: 15%;
  bottom: 20px;
  z-index: 10;
  padding-top: 20px;
  padding-bottom: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
}
.carousel-caption .btn {
  text-shadow: none;
}
@media screen and (min-width: 768px) {
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-prev,
  .carousel-control .icon-next {
    width: 30px;
    height: 30px;
    margin-top: -10px;
    font-size: 30px;
  }
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .icon-prev {
    margin-left: -10px;
  }
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-next {
    margin-right: -10px;
  }
  .carousel-caption {
    left: 20%;
    right: 20%;
    padding-bottom: 30px;
  }
  .carousel-indicators {
    bottom: 20px;
  }
}
.clearfix:before,
.clearfix:after,
.dl-horizontal dd:before,
.dl-horizontal dd:after,
.container:before,
.container:after,
.container-fluid:before,
.container-fluid:after,
.row:before,
.row:after,
.form-horizontal .form-group:before,
.form-horizontal .form-group:after,
.btn-toolbar:before,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:before,
.btn-group-vertical > .btn-group:after,
.nav:before,
.nav:after,
.navbar:before,
.navbar:after,
.navbar-header:before,
.navbar-header:after,
.navbar-collapse:before,
.navbar-collapse:after,
.pager:before,
.pager:after,
.panel-body:before,
.panel-body:after,
.modal-header:before,
.modal-header:after,
.modal-footer:before,
.modal-footer:after,
.item_buttons:before,
.item_buttons:after {
  content: " ";
  display: table;
}
.clearfix:after,
.dl-horizontal dd:after,
.container:after,
.container-fluid:after,
.row:after,
.form-horizontal .form-group:after,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:after,
.nav:after,
.navbar:after,
.navbar-header:after,
.navbar-collapse:after,
.pager:after,
.panel-body:after,
.modal-header:after,
.modal-footer:after,
.item_buttons:after {
  clear: both;
}
.center-block {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.pull-right {
  float: right !important;
}
.pull-left {
  float: left !important;
}
.hide {
  display: none !important;
}
.show {
  display: block !important;
}
.invisible {
  visibility: hidden;
}
.text-hide {
  font: 0/0 a;
  color: transparent;
  text-shadow: none;
  background-color: transparent;
  border: 0;
}
.hidden {
  display: none !important;
}
.affix {
  position: fixed;
}
@-ms-viewport {
  width: device-width;
}
.visible-xs,
.visible-sm,
.visible-md,
.visible-lg {
  display: none !important;
}
.visible-xs-block,
.visible-xs-inline,
.visible-xs-inline-block,
.visible-sm-block,
.visible-sm-inline,
.visible-sm-inline-block,
.visible-md-block,
.visible-md-inline,
.visible-md-inline-block,
.visible-lg-block,
.visible-lg-inline,
.visible-lg-inline-block {
  display: none !important;
}
@media (max-width: 767px) {
  .visible-xs {
    display: block !important;
  }
  table.visible-xs {
    display: table !important;
  }
  tr.visible-xs {
    display: table-row !important;
  }
  th.visible-xs,
  td.visible-xs {
    display: table-cell !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-block {
    display: block !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline {
    display: inline !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm {
    display: block !important;
  }
  table.visible-sm {
    display: table !important;
  }
  tr.visible-sm {
    display: table-row !important;
  }
  th.visible-sm,
  td.visible-sm {
    display: table-cell !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-block {
    display: block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline {
    display: inline !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md {
    display: block !important;
  }
  table.visible-md {
    display: table !important;
  }
  tr.visible-md {
    display: table-row !important;
  }
  th.visible-md,
  td.visible-md {
    display: table-cell !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-block {
    display: block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline {
    display: inline !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg {
    display: block !important;
  }
  table.visible-lg {
    display: table !important;
  }
  tr.visible-lg {
    display: table-row !important;
  }
  th.visible-lg,
  td.visible-lg {
    display: table-cell !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-block {
    display: block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline {
    display: inline !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline-block {
    display: inline-block !important;
  }
}
@media (max-width: 767px) {
  .hidden-xs {
    display: none !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .hidden-sm {
    display: none !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .hidden-md {
    display: none !important;
  }
}
@media (min-width: 1200px) {
  .hidden-lg {
    display: none !important;
  }
}
.visible-print {
  display: none !important;
}
@media print {
  .visible-print {
    display: block !important;
  }
  table.visible-print {
    display: table !important;
  }
  tr.visible-print {
    display: table-row !important;
  }
  th.visible-print,
  td.visible-print {
    display: table-cell !important;
  }
}
.visible-print-block {
  display: none !important;
}
@media print {
  .visible-print-block {
    display: block !important;
  }
}
.visible-print-inline {
  display: none !important;
}
@media print {
  .visible-print-inline {
    display: inline !important;
  }
}
.visible-print-inline-block {
  display: none !important;
}
@media print {
  .visible-print-inline-block {
    display: inline-block !important;
  }
}
@media print {
  .hidden-print {
    display: none !important;
  }
}
/*!
*
* Font Awesome
*
*/
/*!
 *  Font Awesome 4.7.0 by @davegandy - http://fontawesome.io - @fontawesome
 *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
 */
/* FONT PATH
 * -------------------------- */
@font-face {
  font-family: 'FontAwesome';
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?v=4.7.0');
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.7.0') format('embedded-opentype'), url('../components/font-awesome/fonts/fontawesome-webfont.woff2?v=4.7.0') format('woff2'), url('../components/font-awesome/fonts/fontawesome-webfont.woff?v=4.7.0') format('woff'), url('../components/font-awesome/fonts/fontawesome-webfont.ttf?v=4.7.0') format('truetype'), url('../components/font-awesome/fonts/fontawesome-webfont.svg?v=4.7.0#fontawesomeregular') format('svg');
  font-weight: normal;
  font-style: normal;
}
.fa {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
/* makes the font 33% larger relative to the icon container */
.fa-lg {
  font-size: 1.33333333em;
  line-height: 0.75em;
  vertical-align: -15%;
}
.fa-2x {
  font-size: 2em;
}
.fa-3x {
  font-size: 3em;
}
.fa-4x {
  font-size: 4em;
}
.fa-5x {
  font-size: 5em;
}
.fa-fw {
  width: 1.28571429em;
  text-align: center;
}
.fa-ul {
  padding-left: 0;
  margin-left: 2.14285714em;
  list-style-type: none;
}
.fa-ul > li {
  position: relative;
}
.fa-li {
  position: absolute;
  left: -2.14285714em;
  width: 2.14285714em;
  top: 0.14285714em;
  text-align: center;
}
.fa-li.fa-lg {
  left: -1.85714286em;
}
.fa-border {
  padding: .2em .25em .15em;
  border: solid 0.08em #eee;
  border-radius: .1em;
}
.fa-pull-left {
  float: left;
}
.fa-pull-right {
  float: right;
}
.fa.fa-pull-left {
  margin-right: .3em;
}
.fa.fa-pull-right {
  margin-left: .3em;
}
/* Deprecated as of 4.4.0 */
.pull-right {
  float: right;
}
.pull-left {
  float: left;
}
.fa.pull-left {
  margin-right: .3em;
}
.fa.pull-right {
  margin-left: .3em;
}
.fa-spin {
  -webkit-animation: fa-spin 2s infinite linear;
  animation: fa-spin 2s infinite linear;
}
.fa-pulse {
  -webkit-animation: fa-spin 1s infinite steps(8);
  animation: fa-spin 1s infinite steps(8);
}
@-webkit-keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
@keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
.fa-rotate-90 {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=1)";
  -webkit-transform: rotate(90deg);
  -ms-transform: rotate(90deg);
  transform: rotate(90deg);
}
.fa-rotate-180 {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=2)";
  -webkit-transform: rotate(180deg);
  -ms-transform: rotate(180deg);
  transform: rotate(180deg);
}
.fa-rotate-270 {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=3)";
  -webkit-transform: rotate(270deg);
  -ms-transform: rotate(270deg);
  transform: rotate(270deg);
}
.fa-flip-horizontal {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=0, mirror=1)";
  -webkit-transform: scale(-1, 1);
  -ms-transform: scale(-1, 1);
  transform: scale(-1, 1);
}
.fa-flip-vertical {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=2, mirror=1)";
  -webkit-transform: scale(1, -1);
  -ms-transform: scale(1, -1);
  transform: scale(1, -1);
}
:root .fa-rotate-90,
:root .fa-rotate-180,
:root .fa-rotate-270,
:root .fa-flip-horizontal,
:root .fa-flip-vertical {
  filter: none;
}
.fa-stack {
  position: relative;
  display: inline-block;
  width: 2em;
  height: 2em;
  line-height: 2em;
  vertical-align: middle;
}
.fa-stack-1x,
.fa-stack-2x {
  position: absolute;
  left: 0;
  width: 100%;
  text-align: center;
}
.fa-stack-1x {
  line-height: inherit;
}
.fa-stack-2x {
  font-size: 2em;
}
.fa-inverse {
  color: #fff;
}
/* Font Awesome uses the Unicode Private Use Area (PUA) to ensure screen
   readers do not read off random characters that represent icons */
.fa-glass:before {
  content: "\f000";
}
.fa-music:before {
  content: "\f001";
}
.fa-search:before {
  content: "\f002";
}
.fa-envelope-o:before {
  content: "\f003";
}
.fa-heart:before {
  content: "\f004";
}
.fa-star:before {
  content: "\f005";
}
.fa-star-o:before {
  content: "\f006";
}
.fa-user:before {
  content: "\f007";
}
.fa-film:before {
  content: "\f008";
}
.fa-th-large:before {
  content: "\f009";
}
.fa-th:before {
  content: "\f00a";
}
.fa-th-list:before {
  content: "\f00b";
}
.fa-check:before {
  content: "\f00c";
}
.fa-remove:before,
.fa-close:before,
.fa-times:before {
  content: "\f00d";
}
.fa-search-plus:before {
  content: "\f00e";
}
.fa-search-minus:before {
  content: "\f010";
}
.fa-power-off:before {
  content: "\f011";
}
.fa-signal:before {
  content: "\f012";
}
.fa-gear:before,
.fa-cog:before {
  content: "\f013";
}
.fa-trash-o:before {
  content: "\f014";
}
.fa-home:before {
  content: "\f015";
}
.fa-file-o:before {
  content: "\f016";
}
.fa-clock-o:before {
  content: "\f017";
}
.fa-road:before {
  content: "\f018";
}
.fa-download:before {
  content: "\f019";
}
.fa-arrow-circle-o-down:before {
  content: "\f01a";
}
.fa-arrow-circle-o-up:before {
  content: "\f01b";
}
.fa-inbox:before {
  content: "\f01c";
}
.fa-play-circle-o:before {
  content: "\f01d";
}
.fa-rotate-right:before,
.fa-repeat:before {
  content: "\f01e";
}
.fa-refresh:before {
  content: "\f021";
}
.fa-list-alt:before {
  content: "\f022";
}
.fa-lock:before {
  content: "\f023";
}
.fa-flag:before {
  content: "\f024";
}
.fa-headphones:before {
  content: "\f025";
}
.fa-volume-off:before {
  content: "\f026";
}
.fa-volume-down:before {
  content: "\f027";
}
.fa-volume-up:before {
  content: "\f028";
}
.fa-qrcode:before {
  content: "\f029";
}
.fa-barcode:before {
  content: "\f02a";
}
.fa-tag:before {
  content: "\f02b";
}
.fa-tags:before {
  content: "\f02c";
}
.fa-book:before {
  content: "\f02d";
}
.fa-bookmark:before {
  content: "\f02e";
}
.fa-print:before {
  content: "\f02f";
}
.fa-camera:before {
  content: "\f030";
}
.fa-font:before {
  content: "\f031";
}
.fa-bold:before {
  content: "\f032";
}
.fa-italic:before {
  content: "\f033";
}
.fa-text-height:before {
  content: "\f034";
}
.fa-text-width:before {
  content: "\f035";
}
.fa-align-left:before {
  content: "\f036";
}
.fa-align-center:before {
  content: "\f037";
}
.fa-align-right:before {
  content: "\f038";
}
.fa-align-justify:before {
  content: "\f039";
}
.fa-list:before {
  content: "\f03a";
}
.fa-dedent:before,
.fa-outdent:before {
  content: "\f03b";
}
.fa-indent:before {
  content: "\f03c";
}
.fa-video-camera:before {
  content: "\f03d";
}
.fa-photo:before,
.fa-image:before,
.fa-picture-o:before {
  content: "\f03e";
}
.fa-pencil:before {
  content: "\f040";
}
.fa-map-marker:before {
  content: "\f041";
}
.fa-adjust:before {
  content: "\f042";
}
.fa-tint:before {
  content: "\f043";
}
.fa-edit:before,
.fa-pencil-square-o:before {
  content: "\f044";
}
.fa-share-square-o:before {
  content: "\f045";
}
.fa-check-square-o:before {
  content: "\f046";
}
.fa-arrows:before {
  content: "\f047";
}
.fa-step-backward:before {
  content: "\f048";
}
.fa-fast-backward:before {
  content: "\f049";
}
.fa-backward:before {
  content: "\f04a";
}
.fa-play:before {
  content: "\f04b";
}
.fa-pause:before {
  content: "\f04c";
}
.fa-stop:before {
  content: "\f04d";
}
.fa-forward:before {
  content: "\f04e";
}
.fa-fast-forward:before {
  content: "\f050";
}
.fa-step-forward:before {
  content: "\f051";
}
.fa-eject:before {
  content: "\f052";
}
.fa-chevron-left:before {
  content: "\f053";
}
.fa-chevron-right:before {
  content: "\f054";
}
.fa-plus-circle:before {
  content: "\f055";
}
.fa-minus-circle:before {
  content: "\f056";
}
.fa-times-circle:before {
  content: "\f057";
}
.fa-check-circle:before {
  content: "\f058";
}
.fa-question-circle:before {
  content: "\f059";
}
.fa-info-circle:before {
  content: "\f05a";
}
.fa-crosshairs:before {
  content: "\f05b";
}
.fa-times-circle-o:before {
  content: "\f05c";
}
.fa-check-circle-o:before {
  content: "\f05d";
}
.fa-ban:before {
  content: "\f05e";
}
.fa-arrow-left:before {
  content: "\f060";
}
.fa-arrow-right:before {
  content: "\f061";
}
.fa-arrow-up:before {
  content: "\f062";
}
.fa-arrow-down:before {
  content: "\f063";
}
.fa-mail-forward:before,
.fa-share:before {
  content: "\f064";
}
.fa-expand:before {
  content: "\f065";
}
.fa-compress:before {
  content: "\f066";
}
.fa-plus:before {
  content: "\f067";
}
.fa-minus:before {
  content: "\f068";
}
.fa-asterisk:before {
  content: "\f069";
}
.fa-exclamation-circle:before {
  content: "\f06a";
}
.fa-gift:before {
  content: "\f06b";
}
.fa-leaf:before {
  content: "\f06c";
}
.fa-fire:before {
  content: "\f06d";
}
.fa-eye:before {
  content: "\f06e";
}
.fa-eye-slash:before {
  content: "\f070";
}
.fa-warning:before,
.fa-exclamation-triangle:before {
  content: "\f071";
}
.fa-plane:before {
  content: "\f072";
}
.fa-calendar:before {
  content: "\f073";
}
.fa-random:before {
  content: "\f074";
}
.fa-comment:before {
  content: "\f075";
}
.fa-magnet:before {
  content: "\f076";
}
.fa-chevron-up:before {
  content: "\f077";
}
.fa-chevron-down:before {
  content: "\f078";
}
.fa-retweet:before {
  content: "\f079";
}
.fa-shopping-cart:before {
  content: "\f07a";
}
.fa-folder:before {
  content: "\f07b";
}
.fa-folder-open:before {
  content: "\f07c";
}
.fa-arrows-v:before {
  content: "\f07d";
}
.fa-arrows-h:before {
  content: "\f07e";
}
.fa-bar-chart-o:before,
.fa-bar-chart:before {
  content: "\f080";
}
.fa-twitter-square:before {
  content: "\f081";
}
.fa-facebook-square:before {
  content: "\f082";
}
.fa-camera-retro:before {
  content: "\f083";
}
.fa-key:before {
  content: "\f084";
}
.fa-gears:before,
.fa-cogs:before {
  content: "\f085";
}
.fa-comments:before {
  content: "\f086";
}
.fa-thumbs-o-up:before {
  content: "\f087";
}
.fa-thumbs-o-down:before {
  content: "\f088";
}
.fa-star-half:before {
  content: "\f089";
}
.fa-heart-o:before {
  content: "\f08a";
}
.fa-sign-out:before {
  content: "\f08b";
}
.fa-linkedin-square:before {
  content: "\f08c";
}
.fa-thumb-tack:before {
  content: "\f08d";
}
.fa-external-link:before {
  content: "\f08e";
}
.fa-sign-in:before {
  content: "\f090";
}
.fa-trophy:before {
  content: "\f091";
}
.fa-github-square:before {
  content: "\f092";
}
.fa-upload:before {
  content: "\f093";
}
.fa-lemon-o:before {
  content: "\f094";
}
.fa-phone:before {
  content: "\f095";
}
.fa-square-o:before {
  content: "\f096";
}
.fa-bookmark-o:before {
  content: "\f097";
}
.fa-phone-square:before {
  content: "\f098";
}
.fa-twitter:before {
  content: "\f099";
}
.fa-facebook-f:before,
.fa-facebook:before {
  content: "\f09a";
}
.fa-github:before {
  content: "\f09b";
}
.fa-unlock:before {
  content: "\f09c";
}
.fa-credit-card:before {
  content: "\f09d";
}
.fa-feed:before,
.fa-rss:before {
  content: "\f09e";
}
.fa-hdd-o:before {
  content: "\f0a0";
}
.fa-bullhorn:before {
  content: "\f0a1";
}
.fa-bell:before {
  content: "\f0f3";
}
.fa-certificate:before {
  content: "\f0a3";
}
.fa-hand-o-right:before {
  content: "\f0a4";
}
.fa-hand-o-left:before {
  content: "\f0a5";
}
.fa-hand-o-up:before {
  content: "\f0a6";
}
.fa-hand-o-down:before {
  content: "\f0a7";
}
.fa-arrow-circle-left:before {
  content: "\f0a8";
}
.fa-arrow-circle-right:before {
  content: "\f0a9";
}
.fa-arrow-circle-up:before {
  content: "\f0aa";
}
.fa-arrow-circle-down:before {
  content: "\f0ab";
}
.fa-globe:before {
  content: "\f0ac";
}
.fa-wrench:before {
  content: "\f0ad";
}
.fa-tasks:before {
  content: "\f0ae";
}
.fa-filter:before {
  content: "\f0b0";
}
.fa-briefcase:before {
  content: "\f0b1";
}
.fa-arrows-alt:before {
  content: "\f0b2";
}
.fa-group:before,
.fa-users:before {
  content: "\f0c0";
}
.fa-chain:before,
.fa-link:before {
  content: "\f0c1";
}
.fa-cloud:before {
  content: "\f0c2";
}
.fa-flask:before {
  content: "\f0c3";
}
.fa-cut:before,
.fa-scissors:before {
  content: "\f0c4";
}
.fa-copy:before,
.fa-files-o:before {
  content: "\f0c5";
}
.fa-paperclip:before {
  content: "\f0c6";
}
.fa-save:before,
.fa-floppy-o:before {
  content: "\f0c7";
}
.fa-square:before {
  content: "\f0c8";
}
.fa-navicon:before,
.fa-reorder:before,
.fa-bars:before {
  content: "\f0c9";
}
.fa-list-ul:before {
  content: "\f0ca";
}
.fa-list-ol:before {
  content: "\f0cb";
}
.fa-strikethrough:before {
  content: "\f0cc";
}
.fa-underline:before {
  content: "\f0cd";
}
.fa-table:before {
  content: "\f0ce";
}
.fa-magic:before {
  content: "\f0d0";
}
.fa-truck:before {
  content: "\f0d1";
}
.fa-pinterest:before {
  content: "\f0d2";
}
.fa-pinterest-square:before {
  content: "\f0d3";
}
.fa-google-plus-square:before {
  content: "\f0d4";
}
.fa-google-plus:before {
  content: "\f0d5";
}
.fa-money:before {
  content: "\f0d6";
}
.fa-caret-down:before {
  content: "\f0d7";
}
.fa-caret-up:before {
  content: "\f0d8";
}
.fa-caret-left:before {
  content: "\f0d9";
}
.fa-caret-right:before {
  content: "\f0da";
}
.fa-columns:before {
  content: "\f0db";
}
.fa-unsorted:before,
.fa-sort:before {
  content: "\f0dc";
}
.fa-sort-down:before,
.fa-sort-desc:before {
  content: "\f0dd";
}
.fa-sort-up:before,
.fa-sort-asc:before {
  content: "\f0de";
}
.fa-envelope:before {
  content: "\f0e0";
}
.fa-linkedin:before {
  content: "\f0e1";
}
.fa-rotate-left:before,
.fa-undo:before {
  content: "\f0e2";
}
.fa-legal:before,
.fa-gavel:before {
  content: "\f0e3";
}
.fa-dashboard:before,
.fa-tachometer:before {
  content: "\f0e4";
}
.fa-comment-o:before {
  content: "\f0e5";
}
.fa-comments-o:before {
  content: "\f0e6";
}
.fa-flash:before,
.fa-bolt:before {
  content: "\f0e7";
}
.fa-sitemap:before {
  content: "\f0e8";
}
.fa-umbrella:before {
  content: "\f0e9";
}
.fa-paste:before,
.fa-clipboard:before {
  content: "\f0ea";
}
.fa-lightbulb-o:before {
  content: "\f0eb";
}
.fa-exchange:before {
  content: "\f0ec";
}
.fa-cloud-download:before {
  content: "\f0ed";
}
.fa-cloud-upload:before {
  content: "\f0ee";
}
.fa-user-md:before {
  content: "\f0f0";
}
.fa-stethoscope:before {
  content: "\f0f1";
}
.fa-suitcase:before {
  content: "\f0f2";
}
.fa-bell-o:before {
  content: "\f0a2";
}
.fa-coffee:before {
  content: "\f0f4";
}
.fa-cutlery:before {
  content: "\f0f5";
}
.fa-file-text-o:before {
  content: "\f0f6";
}
.fa-building-o:before {
  content: "\f0f7";
}
.fa-hospital-o:before {
  content: "\f0f8";
}
.fa-ambulance:before {
  content: "\f0f9";
}
.fa-medkit:before {
  content: "\f0fa";
}
.fa-fighter-jet:before {
  content: "\f0fb";
}
.fa-beer:before {
  content: "\f0fc";
}
.fa-h-square:before {
  content: "\f0fd";
}
.fa-plus-square:before {
  content: "\f0fe";
}
.fa-angle-double-left:before {
  content: "\f100";
}
.fa-angle-double-right:before {
  content: "\f101";
}
.fa-angle-double-up:before {
  content: "\f102";
}
.fa-angle-double-down:before {
  content: "\f103";
}
.fa-angle-left:before {
  content: "\f104";
}
.fa-angle-right:before {
  content: "\f105";
}
.fa-angle-up:before {
  content: "\f106";
}
.fa-angle-down:before {
  content: "\f107";
}
.fa-desktop:before {
  content: "\f108";
}
.fa-laptop:before {
  content: "\f109";
}
.fa-tablet:before {
  content: "\f10a";
}
.fa-mobile-phone:before,
.fa-mobile:before {
  content: "\f10b";
}
.fa-circle-o:before {
  content: "\f10c";
}
.fa-quote-left:before {
  content: "\f10d";
}
.fa-quote-right:before {
  content: "\f10e";
}
.fa-spinner:before {
  content: "\f110";
}
.fa-circle:before {
  content: "\f111";
}
.fa-mail-reply:before,
.fa-reply:before {
  content: "\f112";
}
.fa-github-alt:before {
  content: "\f113";
}
.fa-folder-o:before {
  content: "\f114";
}
.fa-folder-open-o:before {
  content: "\f115";
}
.fa-smile-o:before {
  content: "\f118";
}
.fa-frown-o:before {
  content: "\f119";
}
.fa-meh-o:before {
  content: "\f11a";
}
.fa-gamepad:before {
  content: "\f11b";
}
.fa-keyboard-o:before {
  content: "\f11c";
}
.fa-flag-o:before {
  content: "\f11d";
}
.fa-flag-checkered:before {
  content: "\f11e";
}
.fa-terminal:before {
  content: "\f120";
}
.fa-code:before {
  content: "\f121";
}
.fa-mail-reply-all:before,
.fa-reply-all:before {
  content: "\f122";
}
.fa-star-half-empty:before,
.fa-star-half-full:before,
.fa-star-half-o:before {
  content: "\f123";
}
.fa-location-arrow:before {
  content: "\f124";
}
.fa-crop:before {
  content: "\f125";
}
.fa-code-fork:before {
  content: "\f126";
}
.fa-unlink:before,
.fa-chain-broken:before {
  content: "\f127";
}
.fa-question:before {
  content: "\f128";
}
.fa-info:before {
  content: "\f129";
}
.fa-exclamation:before {
  content: "\f12a";
}
.fa-superscript:before {
  content: "\f12b";
}
.fa-subscript:before {
  content: "\f12c";
}
.fa-eraser:before {
  content: "\f12d";
}
.fa-puzzle-piece:before {
  content: "\f12e";
}
.fa-microphone:before {
  content: "\f130";
}
.fa-microphone-slash:before {
  content: "\f131";
}
.fa-shield:before {
  content: "\f132";
}
.fa-calendar-o:before {
  content: "\f133";
}
.fa-fire-extinguisher:before {
  content: "\f134";
}
.fa-rocket:before {
  content: "\f135";
}
.fa-maxcdn:before {
  content: "\f136";
}
.fa-chevron-circle-left:before {
  content: "\f137";
}
.fa-chevron-circle-right:before {
  content: "\f138";
}
.fa-chevron-circle-up:before {
  content: "\f139";
}
.fa-chevron-circle-down:before {
  content: "\f13a";
}
.fa-html5:before {
  content: "\f13b";
}
.fa-css3:before {
  content: "\f13c";
}
.fa-anchor:before {
  content: "\f13d";
}
.fa-unlock-alt:before {
  content: "\f13e";
}
.fa-bullseye:before {
  content: "\f140";
}
.fa-ellipsis-h:before {
  content: "\f141";
}
.fa-ellipsis-v:before {
  content: "\f142";
}
.fa-rss-square:before {
  content: "\f143";
}
.fa-play-circle:before {
  content: "\f144";
}
.fa-ticket:before {
  content: "\f145";
}
.fa-minus-square:before {
  content: "\f146";
}
.fa-minus-square-o:before {
  content: "\f147";
}
.fa-level-up:before {
  content: "\f148";
}
.fa-level-down:before {
  content: "\f149";
}
.fa-check-square:before {
  content: "\f14a";
}
.fa-pencil-square:before {
  content: "\f14b";
}
.fa-external-link-square:before {
  content: "\f14c";
}
.fa-share-square:before {
  content: "\f14d";
}
.fa-compass:before {
  content: "\f14e";
}
.fa-toggle-down:before,
.fa-caret-square-o-down:before {
  content: "\f150";
}
.fa-toggle-up:before,
.fa-caret-square-o-up:before {
  content: "\f151";
}
.fa-toggle-right:before,
.fa-caret-square-o-right:before {
  content: "\f152";
}
.fa-euro:before,
.fa-eur:before {
  content: "\f153";
}
.fa-gbp:before {
  content: "\f154";
}
.fa-dollar:before,
.fa-usd:before {
  content: "\f155";
}
.fa-rupee:before,
.fa-inr:before {
  content: "\f156";
}
.fa-cny:before,
.fa-rmb:before,
.fa-yen:before,
.fa-jpy:before {
  content: "\f157";
}
.fa-ruble:before,
.fa-rouble:before,
.fa-rub:before {
  content: "\f158";
}
.fa-won:before,
.fa-krw:before {
  content: "\f159";
}
.fa-bitcoin:before,
.fa-btc:before {
  content: "\f15a";
}
.fa-file:before {
  content: "\f15b";
}
.fa-file-text:before {
  content: "\f15c";
}
.fa-sort-alpha-asc:before {
  content: "\f15d";
}
.fa-sort-alpha-desc:before {
  content: "\f15e";
}
.fa-sort-amount-asc:before {
  content: "\f160";
}
.fa-sort-amount-desc:before {
  content: "\f161";
}
.fa-sort-numeric-asc:before {
  content: "\f162";
}
.fa-sort-numeric-desc:before {
  content: "\f163";
}
.fa-thumbs-up:before {
  content: "\f164";
}
.fa-thumbs-down:before {
  content: "\f165";
}
.fa-youtube-square:before {
  content: "\f166";
}
.fa-youtube:before {
  content: "\f167";
}
.fa-xing:before {
  content: "\f168";
}
.fa-xing-square:before {
  content: "\f169";
}
.fa-youtube-play:before {
  content: "\f16a";
}
.fa-dropbox:before {
  content: "\f16b";
}
.fa-stack-overflow:before {
  content: "\f16c";
}
.fa-instagram:before {
  content: "\f16d";
}
.fa-flickr:before {
  content: "\f16e";
}
.fa-adn:before {
  content: "\f170";
}
.fa-bitbucket:before {
  content: "\f171";
}
.fa-bitbucket-square:before {
  content: "\f172";
}
.fa-tumblr:before {
  content: "\f173";
}
.fa-tumblr-square:before {
  content: "\f174";
}
.fa-long-arrow-down:before {
  content: "\f175";
}
.fa-long-arrow-up:before {
  content: "\f176";
}
.fa-long-arrow-left:before {
  content: "\f177";
}
.fa-long-arrow-right:before {
  content: "\f178";
}
.fa-apple:before {
  content: "\f179";
}
.fa-windows:before {
  content: "\f17a";
}
.fa-android:before {
  content: "\f17b";
}
.fa-linux:before {
  content: "\f17c";
}
.fa-dribbble:before {
  content: "\f17d";
}
.fa-skype:before {
  content: "\f17e";
}
.fa-foursquare:before {
  content: "\f180";
}
.fa-trello:before {
  content: "\f181";
}
.fa-female:before {
  content: "\f182";
}
.fa-male:before {
  content: "\f183";
}
.fa-gittip:before,
.fa-gratipay:before {
  content: "\f184";
}
.fa-sun-o:before {
  content: "\f185";
}
.fa-moon-o:before {
  content: "\f186";
}
.fa-archive:before {
  content: "\f187";
}
.fa-bug:before {
  content: "\f188";
}
.fa-vk:before {
  content: "\f189";
}
.fa-weibo:before {
  content: "\f18a";
}
.fa-renren:before {
  content: "\f18b";
}
.fa-pagelines:before {
  content: "\f18c";
}
.fa-stack-exchange:before {
  content: "\f18d";
}
.fa-arrow-circle-o-right:before {
  content: "\f18e";
}
.fa-arrow-circle-o-left:before {
  content: "\f190";
}
.fa-toggle-left:before,
.fa-caret-square-o-left:before {
  content: "\f191";
}
.fa-dot-circle-o:before {
  content: "\f192";
}
.fa-wheelchair:before {
  content: "\f193";
}
.fa-vimeo-square:before {
  content: "\f194";
}
.fa-turkish-lira:before,
.fa-try:before {
  content: "\f195";
}
.fa-plus-square-o:before {
  content: "\f196";
}
.fa-space-shuttle:before {
  content: "\f197";
}
.fa-slack:before {
  content: "\f198";
}
.fa-envelope-square:before {
  content: "\f199";
}
.fa-wordpress:before {
  content: "\f19a";
}
.fa-openid:before {
  content: "\f19b";
}
.fa-institution:before,
.fa-bank:before,
.fa-university:before {
  content: "\f19c";
}
.fa-mortar-board:before,
.fa-graduation-cap:before {
  content: "\f19d";
}
.fa-yahoo:before {
  content: "\f19e";
}
.fa-google:before {
  content: "\f1a0";
}
.fa-reddit:before {
  content: "\f1a1";
}
.fa-reddit-square:before {
  content: "\f1a2";
}
.fa-stumbleupon-circle:before {
  content: "\f1a3";
}
.fa-stumbleupon:before {
  content: "\f1a4";
}
.fa-delicious:before {
  content: "\f1a5";
}
.fa-digg:before {
  content: "\f1a6";
}
.fa-pied-piper-pp:before {
  content: "\f1a7";
}
.fa-pied-piper-alt:before {
  content: "\f1a8";
}
.fa-drupal:before {
  content: "\f1a9";
}
.fa-joomla:before {
  content: "\f1aa";
}
.fa-language:before {
  content: "\f1ab";
}
.fa-fax:before {
  content: "\f1ac";
}
.fa-building:before {
  content: "\f1ad";
}
.fa-child:before {
  content: "\f1ae";
}
.fa-paw:before {
  content: "\f1b0";
}
.fa-spoon:before {
  content: "\f1b1";
}
.fa-cube:before {
  content: "\f1b2";
}
.fa-cubes:before {
  content: "\f1b3";
}
.fa-behance:before {
  content: "\f1b4";
}
.fa-behance-square:before {
  content: "\f1b5";
}
.fa-steam:before {
  content: "\f1b6";
}
.fa-steam-square:before {
  content: "\f1b7";
}
.fa-recycle:before {
  content: "\f1b8";
}
.fa-automobile:before,
.fa-car:before {
  content: "\f1b9";
}
.fa-cab:before,
.fa-taxi:before {
  content: "\f1ba";
}
.fa-tree:before {
  content: "\f1bb";
}
.fa-spotify:before {
  content: "\f1bc";
}
.fa-deviantart:before {
  content: "\f1bd";
}
.fa-soundcloud:before {
  content: "\f1be";
}
.fa-database:before {
  content: "\f1c0";
}
.fa-file-pdf-o:before {
  content: "\f1c1";
}
.fa-file-word-o:before {
  content: "\f1c2";
}
.fa-file-excel-o:before {
  content: "\f1c3";
}
.fa-file-powerpoint-o:before {
  content: "\f1c4";
}
.fa-file-photo-o:before,
.fa-file-picture-o:before,
.fa-file-image-o:before {
  content: "\f1c5";
}
.fa-file-zip-o:before,
.fa-file-archive-o:before {
  content: "\f1c6";
}
.fa-file-sound-o:before,
.fa-file-audio-o:before {
  content: "\f1c7";
}
.fa-file-movie-o:before,
.fa-file-video-o:before {
  content: "\f1c8";
}
.fa-file-code-o:before {
  content: "\f1c9";
}
.fa-vine:before {
  content: "\f1ca";
}
.fa-codepen:before {
  content: "\f1cb";
}
.fa-jsfiddle:before {
  content: "\f1cc";
}
.fa-life-bouy:before,
.fa-life-buoy:before,
.fa-life-saver:before,
.fa-support:before,
.fa-life-ring:before {
  content: "\f1cd";
}
.fa-circle-o-notch:before {
  content: "\f1ce";
}
.fa-ra:before,
.fa-resistance:before,
.fa-rebel:before {
  content: "\f1d0";
}
.fa-ge:before,
.fa-empire:before {
  content: "\f1d1";
}
.fa-git-square:before {
  content: "\f1d2";
}
.fa-git:before {
  content: "\f1d3";
}
.fa-y-combinator-square:before,
.fa-yc-square:before,
.fa-hacker-news:before {
  content: "\f1d4";
}
.fa-tencent-weibo:before {
  content: "\f1d5";
}
.fa-qq:before {
  content: "\f1d6";
}
.fa-wechat:before,
.fa-weixin:before {
  content: "\f1d7";
}
.fa-send:before,
.fa-paper-plane:before {
  content: "\f1d8";
}
.fa-send-o:before,
.fa-paper-plane-o:before {
  content: "\f1d9";
}
.fa-history:before {
  content: "\f1da";
}
.fa-circle-thin:before {
  content: "\f1db";
}
.fa-header:before {
  content: "\f1dc";
}
.fa-paragraph:before {
  content: "\f1dd";
}
.fa-sliders:before {
  content: "\f1de";
}
.fa-share-alt:before {
  content: "\f1e0";
}
.fa-share-alt-square:before {
  content: "\f1e1";
}
.fa-bomb:before {
  content: "\f1e2";
}
.fa-soccer-ball-o:before,
.fa-futbol-o:before {
  content: "\f1e3";
}
.fa-tty:before {
  content: "\f1e4";
}
.fa-binoculars:before {
  content: "\f1e5";
}
.fa-plug:before {
  content: "\f1e6";
}
.fa-slideshare:before {
  content: "\f1e7";
}
.fa-twitch:before {
  content: "\f1e8";
}
.fa-yelp:before {
  content: "\f1e9";
}
.fa-newspaper-o:before {
  content: "\f1ea";
}
.fa-wifi:before {
  content: "\f1eb";
}
.fa-calculator:before {
  content: "\f1ec";
}
.fa-paypal:before {
  content: "\f1ed";
}
.fa-google-wallet:before {
  content: "\f1ee";
}
.fa-cc-visa:before {
  content: "\f1f0";
}
.fa-cc-mastercard:before {
  content: "\f1f1";
}
.fa-cc-discover:before {
  content: "\f1f2";
}
.fa-cc-amex:before {
  content: "\f1f3";
}
.fa-cc-paypal:before {
  content: "\f1f4";
}
.fa-cc-stripe:before {
  content: "\f1f5";
}
.fa-bell-slash:before {
  content: "\f1f6";
}
.fa-bell-slash-o:before {
  content: "\f1f7";
}
.fa-trash:before {
  content: "\f1f8";
}
.fa-copyright:before {
  content: "\f1f9";
}
.fa-at:before {
  content: "\f1fa";
}
.fa-eyedropper:before {
  content: "\f1fb";
}
.fa-paint-brush:before {
  content: "\f1fc";
}
.fa-birthday-cake:before {
  content: "\f1fd";
}
.fa-area-chart:before {
  content: "\f1fe";
}
.fa-pie-chart:before {
  content: "\f200";
}
.fa-line-chart:before {
  content: "\f201";
}
.fa-lastfm:before {
  content: "\f202";
}
.fa-lastfm-square:before {
  content: "\f203";
}
.fa-toggle-off:before {
  content: "\f204";
}
.fa-toggle-on:before {
  content: "\f205";
}
.fa-bicycle:before {
  content: "\f206";
}
.fa-bus:before {
  content: "\f207";
}
.fa-ioxhost:before {
  content: "\f208";
}
.fa-angellist:before {
  content: "\f209";
}
.fa-cc:before {
  content: "\f20a";
}
.fa-shekel:before,
.fa-sheqel:before,
.fa-ils:before {
  content: "\f20b";
}
.fa-meanpath:before {
  content: "\f20c";
}
.fa-buysellads:before {
  content: "\f20d";
}
.fa-connectdevelop:before {
  content: "\f20e";
}
.fa-dashcube:before {
  content: "\f210";
}
.fa-forumbee:before {
  content: "\f211";
}
.fa-leanpub:before {
  content: "\f212";
}
.fa-sellsy:before {
  content: "\f213";
}
.fa-shirtsinbulk:before {
  content: "\f214";
}
.fa-simplybuilt:before {
  content: "\f215";
}
.fa-skyatlas:before {
  content: "\f216";
}
.fa-cart-plus:before {
  content: "\f217";
}
.fa-cart-arrow-down:before {
  content: "\f218";
}
.fa-diamond:before {
  content: "\f219";
}
.fa-ship:before {
  content: "\f21a";
}
.fa-user-secret:before {
  content: "\f21b";
}
.fa-motorcycle:before {
  content: "\f21c";
}
.fa-street-view:before {
  content: "\f21d";
}
.fa-heartbeat:before {
  content: "\f21e";
}
.fa-venus:before {
  content: "\f221";
}
.fa-mars:before {
  content: "\f222";
}
.fa-mercury:before {
  content: "\f223";
}
.fa-intersex:before,
.fa-transgender:before {
  content: "\f224";
}
.fa-transgender-alt:before {
  content: "\f225";
}
.fa-venus-double:before {
  content: "\f226";
}
.fa-mars-double:before {
  content: "\f227";
}
.fa-venus-mars:before {
  content: "\f228";
}
.fa-mars-stroke:before {
  content: "\f229";
}
.fa-mars-stroke-v:before {
  content: "\f22a";
}
.fa-mars-stroke-h:before {
  content: "\f22b";
}
.fa-neuter:before {
  content: "\f22c";
}
.fa-genderless:before {
  content: "\f22d";
}
.fa-facebook-official:before {
  content: "\f230";
}
.fa-pinterest-p:before {
  content: "\f231";
}
.fa-whatsapp:before {
  content: "\f232";
}
.fa-server:before {
  content: "\f233";
}
.fa-user-plus:before {
  content: "\f234";
}
.fa-user-times:before {
  content: "\f235";
}
.fa-hotel:before,
.fa-bed:before {
  content: "\f236";
}
.fa-viacoin:before {
  content: "\f237";
}
.fa-train:before {
  content: "\f238";
}
.fa-subway:before {
  content: "\f239";
}
.fa-medium:before {
  content: "\f23a";
}
.fa-yc:before,
.fa-y-combinator:before {
  content: "\f23b";
}
.fa-optin-monster:before {
  content: "\f23c";
}
.fa-opencart:before {
  content: "\f23d";
}
.fa-expeditedssl:before {
  content: "\f23e";
}
.fa-battery-4:before,
.fa-battery:before,
.fa-battery-full:before {
  content: "\f240";
}
.fa-battery-3:before,
.fa-battery-three-quarters:before {
  content: "\f241";
}
.fa-battery-2:before,
.fa-battery-half:before {
  content: "\f242";
}
.fa-battery-1:before,
.fa-battery-quarter:before {
  content: "\f243";
}
.fa-battery-0:before,
.fa-battery-empty:before {
  content: "\f244";
}
.fa-mouse-pointer:before {
  content: "\f245";
}
.fa-i-cursor:before {
  content: "\f246";
}
.fa-object-group:before {
  content: "\f247";
}
.fa-object-ungroup:before {
  content: "\f248";
}
.fa-sticky-note:before {
  content: "\f249";
}
.fa-sticky-note-o:before {
  content: "\f24a";
}
.fa-cc-jcb:before {
  content: "\f24b";
}
.fa-cc-diners-club:before {
  content: "\f24c";
}
.fa-clone:before {
  content: "\f24d";
}
.fa-balance-scale:before {
  content: "\f24e";
}
.fa-hourglass-o:before {
  content: "\f250";
}
.fa-hourglass-1:before,
.fa-hourglass-start:before {
  content: "\f251";
}
.fa-hourglass-2:before,
.fa-hourglass-half:before {
  content: "\f252";
}
.fa-hourglass-3:before,
.fa-hourglass-end:before {
  content: "\f253";
}
.fa-hourglass:before {
  content: "\f254";
}
.fa-hand-grab-o:before,
.fa-hand-rock-o:before {
  content: "\f255";
}
.fa-hand-stop-o:before,
.fa-hand-paper-o:before {
  content: "\f256";
}
.fa-hand-scissors-o:before {
  content: "\f257";
}
.fa-hand-lizard-o:before {
  content: "\f258";
}
.fa-hand-spock-o:before {
  content: "\f259";
}
.fa-hand-pointer-o:before {
  content: "\f25a";
}
.fa-hand-peace-o:before {
  content: "\f25b";
}
.fa-trademark:before {
  content: "\f25c";
}
.fa-registered:before {
  content: "\f25d";
}
.fa-creative-commons:before {
  content: "\f25e";
}
.fa-gg:before {
  content: "\f260";
}
.fa-gg-circle:before {
  content: "\f261";
}
.fa-tripadvisor:before {
  content: "\f262";
}
.fa-odnoklassniki:before {
  content: "\f263";
}
.fa-odnoklassniki-square:before {
  content: "\f264";
}
.fa-get-pocket:before {
  content: "\f265";
}
.fa-wikipedia-w:before {
  content: "\f266";
}
.fa-safari:before {
  content: "\f267";
}
.fa-chrome:before {
  content: "\f268";
}
.fa-firefox:before {
  content: "\f269";
}
.fa-opera:before {
  content: "\f26a";
}
.fa-internet-explorer:before {
  content: "\f26b";
}
.fa-tv:before,
.fa-television:before {
  content: "\f26c";
}
.fa-contao:before {
  content: "\f26d";
}
.fa-500px:before {
  content: "\f26e";
}
.fa-amazon:before {
  content: "\f270";
}
.fa-calendar-plus-o:before {
  content: "\f271";
}
.fa-calendar-minus-o:before {
  content: "\f272";
}
.fa-calendar-times-o:before {
  content: "\f273";
}
.fa-calendar-check-o:before {
  content: "\f274";
}
.fa-industry:before {
  content: "\f275";
}
.fa-map-pin:before {
  content: "\f276";
}
.fa-map-signs:before {
  content: "\f277";
}
.fa-map-o:before {
  content: "\f278";
}
.fa-map:before {
  content: "\f279";
}
.fa-commenting:before {
  content: "\f27a";
}
.fa-commenting-o:before {
  content: "\f27b";
}
.fa-houzz:before {
  content: "\f27c";
}
.fa-vimeo:before {
  content: "\f27d";
}
.fa-black-tie:before {
  content: "\f27e";
}
.fa-fonticons:before {
  content: "\f280";
}
.fa-reddit-alien:before {
  content: "\f281";
}
.fa-edge:before {
  content: "\f282";
}
.fa-credit-card-alt:before {
  content: "\f283";
}
.fa-codiepie:before {
  content: "\f284";
}
.fa-modx:before {
  content: "\f285";
}
.fa-fort-awesome:before {
  content: "\f286";
}
.fa-usb:before {
  content: "\f287";
}
.fa-product-hunt:before {
  content: "\f288";
}
.fa-mixcloud:before {
  content: "\f289";
}
.fa-scribd:before {
  content: "\f28a";
}
.fa-pause-circle:before {
  content: "\f28b";
}
.fa-pause-circle-o:before {
  content: "\f28c";
}
.fa-stop-circle:before {
  content: "\f28d";
}
.fa-stop-circle-o:before {
  content: "\f28e";
}
.fa-shopping-bag:before {
  content: "\f290";
}
.fa-shopping-basket:before {
  content: "\f291";
}
.fa-hashtag:before {
  content: "\f292";
}
.fa-bluetooth:before {
  content: "\f293";
}
.fa-bluetooth-b:before {
  content: "\f294";
}
.fa-percent:before {
  content: "\f295";
}
.fa-gitlab:before {
  content: "\f296";
}
.fa-wpbeginner:before {
  content: "\f297";
}
.fa-wpforms:before {
  content: "\f298";
}
.fa-envira:before {
  content: "\f299";
}
.fa-universal-access:before {
  content: "\f29a";
}
.fa-wheelchair-alt:before {
  content: "\f29b";
}
.fa-question-circle-o:before {
  content: "\f29c";
}
.fa-blind:before {
  content: "\f29d";
}
.fa-audio-description:before {
  content: "\f29e";
}
.fa-volume-control-phone:before {
  content: "\f2a0";
}
.fa-braille:before {
  content: "\f2a1";
}
.fa-assistive-listening-systems:before {
  content: "\f2a2";
}
.fa-asl-interpreting:before,
.fa-american-sign-language-interpreting:before {
  content: "\f2a3";
}
.fa-deafness:before,
.fa-hard-of-hearing:before,
.fa-deaf:before {
  content: "\f2a4";
}
.fa-glide:before {
  content: "\f2a5";
}
.fa-glide-g:before {
  content: "\f2a6";
}
.fa-signing:before,
.fa-sign-language:before {
  content: "\f2a7";
}
.fa-low-vision:before {
  content: "\f2a8";
}
.fa-viadeo:before {
  content: "\f2a9";
}
.fa-viadeo-square:before {
  content: "\f2aa";
}
.fa-snapchat:before {
  content: "\f2ab";
}
.fa-snapchat-ghost:before {
  content: "\f2ac";
}
.fa-snapchat-square:before {
  content: "\f2ad";
}
.fa-pied-piper:before {
  content: "\f2ae";
}
.fa-first-order:before {
  content: "\f2b0";
}
.fa-yoast:before {
  content: "\f2b1";
}
.fa-themeisle:before {
  content: "\f2b2";
}
.fa-google-plus-circle:before,
.fa-google-plus-official:before {
  content: "\f2b3";
}
.fa-fa:before,
.fa-font-awesome:before {
  content: "\f2b4";
}
.fa-handshake-o:before {
  content: "\f2b5";
}
.fa-envelope-open:before {
  content: "\f2b6";
}
.fa-envelope-open-o:before {
  content: "\f2b7";
}
.fa-linode:before {
  content: "\f2b8";
}
.fa-address-book:before {
  content: "\f2b9";
}
.fa-address-book-o:before {
  content: "\f2ba";
}
.fa-vcard:before,
.fa-address-card:before {
  content: "\f2bb";
}
.fa-vcard-o:before,
.fa-address-card-o:before {
  content: "\f2bc";
}
.fa-user-circle:before {
  content: "\f2bd";
}
.fa-user-circle-o:before {
  content: "\f2be";
}
.fa-user-o:before {
  content: "\f2c0";
}
.fa-id-badge:before {
  content: "\f2c1";
}
.fa-drivers-license:before,
.fa-id-card:before {
  content: "\f2c2";
}
.fa-drivers-license-o:before,
.fa-id-card-o:before {
  content: "\f2c3";
}
.fa-quora:before {
  content: "\f2c4";
}
.fa-free-code-camp:before {
  content: "\f2c5";
}
.fa-telegram:before {
  content: "\f2c6";
}
.fa-thermometer-4:before,
.fa-thermometer:before,
.fa-thermometer-full:before {
  content: "\f2c7";
}
.fa-thermometer-3:before,
.fa-thermometer-three-quarters:before {
  content: "\f2c8";
}
.fa-thermometer-2:before,
.fa-thermometer-half:before {
  content: "\f2c9";
}
.fa-thermometer-1:before,
.fa-thermometer-quarter:before {
  content: "\f2ca";
}
.fa-thermometer-0:before,
.fa-thermometer-empty:before {
  content: "\f2cb";
}
.fa-shower:before {
  content: "\f2cc";
}
.fa-bathtub:before,
.fa-s15:before,
.fa-bath:before {
  content: "\f2cd";
}
.fa-podcast:before {
  content: "\f2ce";
}
.fa-window-maximize:before {
  content: "\f2d0";
}
.fa-window-minimize:before {
  content: "\f2d1";
}
.fa-window-restore:before {
  content: "\f2d2";
}
.fa-times-rectangle:before,
.fa-window-close:before {
  content: "\f2d3";
}
.fa-times-rectangle-o:before,
.fa-window-close-o:before {
  content: "\f2d4";
}
.fa-bandcamp:before {
  content: "\f2d5";
}
.fa-grav:before {
  content: "\f2d6";
}
.fa-etsy:before {
  content: "\f2d7";
}
.fa-imdb:before {
  content: "\f2d8";
}
.fa-ravelry:before {
  content: "\f2d9";
}
.fa-eercast:before {
  content: "\f2da";
}
.fa-microchip:before {
  content: "\f2db";
}
.fa-snowflake-o:before {
  content: "\f2dc";
}
.fa-superpowers:before {
  content: "\f2dd";
}
.fa-wpexplorer:before {
  content: "\f2de";
}
.fa-meetup:before {
  content: "\f2e0";
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
/*!
*
* IPython base
*
*/
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
code {
  color: #000;
}
pre {
  font-size: inherit;
  line-height: inherit;
}
label {
  font-weight: normal;
}
/* Make the page background atleast 100% the height of the view port */
/* Make the page itself atleast 70% the height of the view port */
.border-box-sizing {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.corner-all {
  border-radius: 2px;
}
.no-padding {
  padding: 0px;
}
/* Flexible box model classes */
/* Taken from Alex Russell http://infrequently.org/2009/08/css-3-progress/ */
/* This file is a compatability layer.  It allows the usage of flexible box 
model layouts accross multiple browsers, including older browsers.  The newest,
universal implementation of the flexible box model is used when available (see
`Modern browsers` comments below).  Browsers that are known to implement this 
new spec completely include:

    Firefox 28.0+
    Chrome 29.0+
    Internet Explorer 11+ 
    Opera 17.0+

Browsers not listed, including Safari, are supported via the styling under the
`Old browsers` comments below.
*/
.hbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
.hbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.vbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
.vbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.hbox.reverse,
.vbox.reverse,
.reverse {
  /* Old browsers */
  -webkit-box-direction: reverse;
  -moz-box-direction: reverse;
  box-direction: reverse;
  /* Modern browsers */
  flex-direction: row-reverse;
}
.hbox.box-flex0,
.vbox.box-flex0,
.box-flex0 {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
  width: auto;
}
.hbox.box-flex1,
.vbox.box-flex1,
.box-flex1 {
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex,
.vbox.box-flex,
.box-flex {
  /* Old browsers */
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex2,
.vbox.box-flex2,
.box-flex2 {
  /* Old browsers */
  -webkit-box-flex: 2;
  -moz-box-flex: 2;
  box-flex: 2;
  /* Modern browsers */
  flex: 2;
}
.box-group1 {
  /*  Deprecated */
  -webkit-box-flex-group: 1;
  -moz-box-flex-group: 1;
  box-flex-group: 1;
}
.box-group2 {
  /* Deprecated */
  -webkit-box-flex-group: 2;
  -moz-box-flex-group: 2;
  box-flex-group: 2;
}
.hbox.start,
.vbox.start,
.start {
  /* Old browsers */
  -webkit-box-pack: start;
  -moz-box-pack: start;
  box-pack: start;
  /* Modern browsers */
  justify-content: flex-start;
}
.hbox.end,
.vbox.end,
.end {
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
}
.hbox.center,
.vbox.center,
.center {
  /* Old browsers */
  -webkit-box-pack: center;
  -moz-box-pack: center;
  box-pack: center;
  /* Modern browsers */
  justify-content: center;
}
.hbox.baseline,
.vbox.baseline,
.baseline {
  /* Old browsers */
  -webkit-box-pack: baseline;
  -moz-box-pack: baseline;
  box-pack: baseline;
  /* Modern browsers */
  justify-content: baseline;
}
.hbox.stretch,
.vbox.stretch,
.stretch {
  /* Old browsers */
  -webkit-box-pack: stretch;
  -moz-box-pack: stretch;
  box-pack: stretch;
  /* Modern browsers */
  justify-content: stretch;
}
.hbox.align-start,
.vbox.align-start,
.align-start {
  /* Old browsers */
  -webkit-box-align: start;
  -moz-box-align: start;
  box-align: start;
  /* Modern browsers */
  align-items: flex-start;
}
.hbox.align-end,
.vbox.align-end,
.align-end {
  /* Old browsers */
  -webkit-box-align: end;
  -moz-box-align: end;
  box-align: end;
  /* Modern browsers */
  align-items: flex-end;
}
.hbox.align-center,
.vbox.align-center,
.align-center {
  /* Old browsers */
  -webkit-box-align: center;
  -moz-box-align: center;
  box-align: center;
  /* Modern browsers */
  align-items: center;
}
.hbox.align-baseline,
.vbox.align-baseline,
.align-baseline {
  /* Old browsers */
  -webkit-box-align: baseline;
  -moz-box-align: baseline;
  box-align: baseline;
  /* Modern browsers */
  align-items: baseline;
}
.hbox.align-stretch,
.vbox.align-stretch,
.align-stretch {
  /* Old browsers */
  -webkit-box-align: stretch;
  -moz-box-align: stretch;
  box-align: stretch;
  /* Modern browsers */
  align-items: stretch;
}
div.error {
  margin: 2em;
  text-align: center;
}
div.error > h1 {
  font-size: 500%;
  line-height: normal;
}
div.error > p {
  font-size: 200%;
  line-height: normal;
}
div.traceback-wrapper {
  text-align: left;
  max-width: 800px;
  margin: auto;
}
div.traceback-wrapper pre.traceback {
  max-height: 600px;
  overflow: auto;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
body {
  background-color: #fff;
  /* This makes sure that the body covers the entire window and needs to
       be in a different element than the display: box in wrapper below */
  position: absolute;
  left: 0px;
  right: 0px;
  top: 0px;
  bottom: 0px;
  overflow: visible;
}
body > #header {
  /* Initially hidden to prevent FLOUC */
  display: none;
  background-color: #fff;
  /* Display over codemirror */
  position: relative;
  z-index: 100;
}
body > #header #header-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 5px;
  padding-bottom: 5px;
  padding-top: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
body > #header .header-bar {
  width: 100%;
  height: 1px;
  background: #e7e7e7;
  margin-bottom: -1px;
}
@media print {
  body > #header {
    display: none !important;
  }
}
#header-spacer {
  width: 100%;
  visibility: hidden;
}
@media print {
  #header-spacer {
    display: none;
  }
}
#ipython_notebook {
  padding-left: 0px;
  padding-top: 1px;
  padding-bottom: 1px;
}
[dir="rtl"] #ipython_notebook {
  margin-right: 10px;
  margin-left: 0;
}
[dir="rtl"] #ipython_notebook.pull-left {
  float: right !important;
  float: right;
}
.flex-spacer {
  flex: 1;
}
#noscript {
  width: auto;
  padding-top: 16px;
  padding-bottom: 16px;
  text-align: center;
  font-size: 22px;
  color: red;
  font-weight: bold;
}
#ipython_notebook img {
  height: 28px;
}
#site {
  width: 100%;
  display: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  overflow: auto;
}
@media print {
  #site {
    height: auto !important;
  }
}
/* Smaller buttons */
.ui-button .ui-button-text {
  padding: 0.2em 0.8em;
  font-size: 77%;
}
input.ui-button {
  padding: 0.3em 0.9em;
}
span#kernel_logo_widget {
  margin: 0 10px;
}
span#login_widget {
  float: right;
}
[dir="rtl"] span#login_widget {
  float: left;
}
span#login_widget > .button,
#logout {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button:focus,
#logout:focus,
span#login_widget > .button.focus,
#logout.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
span#login_widget > .button:hover,
#logout:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active:hover,
#logout:active:hover,
span#login_widget > .button.active:hover,
#logout.active:hover,
.open > .dropdown-togglespan#login_widget > .button:hover,
.open > .dropdown-toggle#logout:hover,
span#login_widget > .button:active:focus,
#logout:active:focus,
span#login_widget > .button.active:focus,
#logout.active:focus,
.open > .dropdown-togglespan#login_widget > .button:focus,
.open > .dropdown-toggle#logout:focus,
span#login_widget > .button:active.focus,
#logout:active.focus,
span#login_widget > .button.active.focus,
#logout.active.focus,
.open > .dropdown-togglespan#login_widget > .button.focus,
.open > .dropdown-toggle#logout.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  background-image: none;
}
span#login_widget > .button.disabled:hover,
#logout.disabled:hover,
span#login_widget > .button[disabled]:hover,
#logout[disabled]:hover,
fieldset[disabled] span#login_widget > .button:hover,
fieldset[disabled] #logout:hover,
span#login_widget > .button.disabled:focus,
#logout.disabled:focus,
span#login_widget > .button[disabled]:focus,
#logout[disabled]:focus,
fieldset[disabled] span#login_widget > .button:focus,
fieldset[disabled] #logout:focus,
span#login_widget > .button.disabled.focus,
#logout.disabled.focus,
span#login_widget > .button[disabled].focus,
#logout[disabled].focus,
fieldset[disabled] span#login_widget > .button.focus,
fieldset[disabled] #logout.focus {
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button .badge,
#logout .badge {
  color: #fff;
  background-color: #333;
}
.nav-header {
  text-transform: none;
}
#header > span {
  margin-top: 10px;
}
.modal_stretch .modal-dialog {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  min-height: 80vh;
}
.modal_stretch .modal-dialog .modal-body {
  max-height: calc(100vh - 200px);
  overflow: auto;
  flex: 1;
}
.modal-header {
  cursor: move;
}
@media (min-width: 768px) {
  .modal .modal-dialog {
    width: 700px;
  }
}
@media (min-width: 768px) {
  select.form-control {
    margin-left: 12px;
    margin-right: 12px;
  }
}
/*!
*
* IPython auth
*
*/
.center-nav {
  display: inline-block;
  margin-bottom: -4px;
}
[dir="rtl"] .center-nav form.pull-left {
  float: right !important;
  float: right;
}
[dir="rtl"] .center-nav .navbar-text {
  float: right;
}
[dir="rtl"] .navbar-inner {
  text-align: right;
}
[dir="rtl"] div.text-left {
  text-align: right;
}
/*!
*
* IPython tree view
*
*/
/* We need an invisible input field on top of the sentense*/
/* "Drag file onto the list ..." */
.alternate_upload {
  background-color: none;
  display: inline;
}
.alternate_upload.form {
  padding: 0;
  margin: 0;
}
.alternate_upload input.fileinput {
  position: absolute;
  display: block;
  width: 100%;
  height: 100%;
  overflow: hidden;
  cursor: pointer;
  opacity: 0;
  z-index: 2;
}
.alternate_upload .btn-xs > input.fileinput {
  margin: -1px -5px;
}
.alternate_upload .btn-upload {
  position: relative;
  height: 22px;
}
::-webkit-file-upload-button {
  cursor: pointer;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
ul#tabs {
  margin-bottom: 4px;
}
ul#tabs a {
  padding-top: 6px;
  padding-bottom: 4px;
}
[dir="rtl"] ul#tabs.nav-tabs > li {
  float: right;
}
[dir="rtl"] ul#tabs.nav.nav-tabs {
  padding-right: 0;
}
ul.breadcrumb a:focus,
ul.breadcrumb a:hover {
  text-decoration: none;
}
ul.breadcrumb i.icon-home {
  font-size: 16px;
  margin-right: 4px;
}
ul.breadcrumb span {
  color: #5e5e5e;
}
.list_toolbar {
  padding: 4px 0 4px 0;
  vertical-align: middle;
}
.list_toolbar .tree-buttons {
  padding-top: 1px;
}
[dir="rtl"] .list_toolbar .tree-buttons .pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .list_toolbar .col-sm-4,
[dir="rtl"] .list_toolbar .col-sm-8 {
  float: right;
}
.dynamic-buttons {
  padding-top: 3px;
  display: inline-block;
}
.list_toolbar [class*="span"] {
  min-height: 24px;
}
.list_header {
  font-weight: bold;
  background-color: #EEE;
}
.list_placeholder {
  font-weight: bold;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
}
.list_container {
  margin-top: 4px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 2px;
}
.list_container > div {
  border-bottom: 1px solid #ddd;
}
.list_container > div:hover .list-item {
  background-color: red;
}
.list_container > div:last-child {
  border: none;
}
.list_item:hover .list_item {
  background-color: #ddd;
}
.list_item a {
  text-decoration: none;
}
.list_item:hover {
  background-color: #fafafa;
}
.list_header > div,
.list_item > div {
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
.list_header > div input,
.list_item > div input {
  margin-right: 7px;
  margin-left: 14px;
  vertical-align: text-bottom;
  line-height: 22px;
  position: relative;
  top: -1px;
}
.list_header > div .item_link,
.list_item > div .item_link {
  margin-left: -1px;
  vertical-align: baseline;
  line-height: 22px;
}
[dir="rtl"] .list_item > div input {
  margin-right: 0;
}
.new-file input[type=checkbox] {
  visibility: hidden;
}
.item_name {
  line-height: 22px;
  height: 24px;
}
.item_icon {
  font-size: 14px;
  color: #5e5e5e;
  margin-right: 7px;
  margin-left: 7px;
  line-height: 22px;
  vertical-align: baseline;
}
.item_modified {
  margin-right: 7px;
  margin-left: 7px;
}
[dir="rtl"] .item_modified.pull-right {
  float: left !important;
  float: left;
}
.item_buttons {
  line-height: 1em;
  margin-left: -5px;
}
.item_buttons .btn,
.item_buttons .btn-group,
.item_buttons .input-group {
  float: left;
}
.item_buttons > .btn,
.item_buttons > .btn-group,
.item_buttons > .input-group {
  margin-left: 5px;
}
.item_buttons .btn {
  min-width: 13ex;
}
.item_buttons .running-indicator {
  padding-top: 4px;
  color: #5cb85c;
}
.item_buttons .kernel-name {
  padding-top: 4px;
  color: #5bc0de;
  margin-right: 7px;
  float: left;
}
[dir="rtl"] .item_buttons.pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .item_buttons .kernel-name {
  margin-left: 7px;
  float: right;
}
.toolbar_info {
  height: 24px;
  line-height: 24px;
}
.list_item input:not([type=checkbox]) {
  padding-top: 3px;
  padding-bottom: 3px;
  height: 22px;
  line-height: 14px;
  margin: 0px;
}
.highlight_text {
  color: blue;
}
#project_name {
  display: inline-block;
  padding-left: 7px;
  margin-left: -2px;
}
#project_name > .breadcrumb {
  padding: 0px;
  margin-bottom: 0px;
  background-color: transparent;
  font-weight: bold;
}
.sort_button {
  display: inline-block;
  padding-left: 7px;
}
[dir="rtl"] .sort_button.pull-right {
  float: left !important;
  float: left;
}
#tree-selector {
  padding-right: 0px;
}
#button-select-all {
  min-width: 50px;
}
[dir="rtl"] #button-select-all.btn {
  float: right ;
}
#select-all {
  margin-left: 7px;
  margin-right: 2px;
  margin-top: 2px;
  height: 16px;
}
[dir="rtl"] #select-all.pull-left {
  float: right !important;
  float: right;
}
.menu_icon {
  margin-right: 2px;
}
.tab-content .row {
  margin-left: 0px;
  margin-right: 0px;
}
.folder_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f114";
}
.folder_icon:before.fa-pull-left {
  margin-right: .3em;
}
.folder_icon:before.fa-pull-right {
  margin-left: .3em;
}
.folder_icon:before.pull-left {
  margin-right: .3em;
}
.folder_icon:before.pull-right {
  margin-left: .3em;
}
.notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
}
.notebook_icon:before.fa-pull-left {
  margin-right: .3em;
}
.notebook_icon:before.fa-pull-right {
  margin-left: .3em;
}
.notebook_icon:before.pull-left {
  margin-right: .3em;
}
.notebook_icon:before.pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
  color: #5cb85c;
}
.running_notebook_icon:before.fa-pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.fa-pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before.pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.pull-right {
  margin-left: .3em;
}
.file_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f016";
  position: relative;
  top: -2px;
}
.file_icon:before.fa-pull-left {
  margin-right: .3em;
}
.file_icon:before.fa-pull-right {
  margin-left: .3em;
}
.file_icon:before.pull-left {
  margin-right: .3em;
}
.file_icon:before.pull-right {
  margin-left: .3em;
}
#notebook_toolbar .pull-right {
  padding-top: 0px;
  margin-right: -1px;
}
ul#new-menu {
  left: auto;
  right: 0;
}
#new-menu .dropdown-header {
  font-size: 10px;
  border-bottom: 1px solid #e5e5e5;
  padding: 0 0 3px;
  margin: -3px 20px 0;
}
.kernel-menu-icon {
  padding-right: 12px;
  width: 24px;
  content: "\f096";
}
.kernel-menu-icon:before {
  content: "\f096";
}
.kernel-menu-icon-current:before {
  content: "\f00c";
}
#tab_content {
  padding-top: 20px;
}
#running .panel-group .panel {
  margin-top: 3px;
  margin-bottom: 1em;
}
#running .panel-group .panel .panel-heading {
  background-color: #EEE;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
#running .panel-group .panel .panel-heading a:focus,
#running .panel-group .panel .panel-heading a:hover {
  text-decoration: none;
}
#running .panel-group .panel .panel-body {
  padding: 0px;
}
#running .panel-group .panel .panel-body .list_container {
  margin-top: 0px;
  margin-bottom: 0px;
  border: 0px;
  border-radius: 0px;
}
#running .panel-group .panel .panel-body .list_container .list_item {
  border-bottom: 1px solid #ddd;
}
#running .panel-group .panel .panel-body .list_container .list_item:last-child {
  border-bottom: 0px;
}
.delete-button {
  display: none;
}
.duplicate-button {
  display: none;
}
.rename-button {
  display: none;
}
.move-button {
  display: none;
}
.download-button {
  display: none;
}
.shutdown-button {
  display: none;
}
.dynamic-instructions {
  display: inline-block;
  padding-top: 4px;
}
/*!
*
* IPython text editor webapp
*
*/
.selected-keymap i.fa {
  padding: 0px 5px;
}
.selected-keymap i.fa:before {
  content: "\f00c";
}
#mode-menu {
  overflow: auto;
  max-height: 20em;
}
.edit_app #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.edit_app #menubar .navbar {
  /* Use a negative 1 bottom margin, so the border overlaps the border of the
    header */
  margin-bottom: -1px;
}
.dirty-indicator {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator.pull-left {
  margin-right: .3em;
}
.dirty-indicator.pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-dirty.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty.pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-clean.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f00c";
}
.dirty-indicator-clean:before.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.pull-right {
  margin-left: .3em;
}
#filename {
  font-size: 16pt;
  display: table;
  padding: 0px 5px;
}
#current-mode {
  padding-left: 5px;
  padding-right: 5px;
}
#texteditor-backdrop {
  padding-top: 20px;
  padding-bottom: 20px;
}
@media not print {
  #texteditor-backdrop {
    background-color: #EEE;
  }
}
@media print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container {
    padding: 0px;
    background-color: #fff;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
.CodeMirror-dialog {
  background-color: #fff;
}
/*!
*
* IPython notebook
*
*/
/* CSS font colors for translated ANSI escape sequences */
/* The color values are a mix of
   http://www.xcolors.net/dl/baskerville-ivorylight and
   http://www.xcolors.net/dl/euphrasia */
.ansi-black-fg {
  color: #3E424D;
}
.ansi-black-bg {
  background-color: #3E424D;
}
.ansi-black-intense-fg {
  color: #282C36;
}
.ansi-black-intense-bg {
  background-color: #282C36;
}
.ansi-red-fg {
  color: #E75C58;
}
.ansi-red-bg {
  background-color: #E75C58;
}
.ansi-red-intense-fg {
  color: #B22B31;
}
.ansi-red-intense-bg {
  background-color: #B22B31;
}
.ansi-green-fg {
  color: #00A250;
}
.ansi-green-bg {
  background-color: #00A250;
}
.ansi-green-intense-fg {
  color: #007427;
}
.ansi-green-intense-bg {
  background-color: #007427;
}
.ansi-yellow-fg {
  color: #DDB62B;
}
.ansi-yellow-bg {
  background-color: #DDB62B;
}
.ansi-yellow-intense-fg {
  color: #B27D12;
}
.ansi-yellow-intense-bg {
  background-color: #B27D12;
}
.ansi-blue-fg {
  color: #208FFB;
}
.ansi-blue-bg {
  background-color: #208FFB;
}
.ansi-blue-intense-fg {
  color: #0065CA;
}
.ansi-blue-intense-bg {
  background-color: #0065CA;
}
.ansi-magenta-fg {
  color: #D160C4;
}
.ansi-magenta-bg {
  background-color: #D160C4;
}
.ansi-magenta-intense-fg {
  color: #A03196;
}
.ansi-magenta-intense-bg {
  background-color: #A03196;
}
.ansi-cyan-fg {
  color: #60C6C8;
}
.ansi-cyan-bg {
  background-color: #60C6C8;
}
.ansi-cyan-intense-fg {
  color: #258F8F;
}
.ansi-cyan-intense-bg {
  background-color: #258F8F;
}
.ansi-white-fg {
  color: #C5C1B4;
}
.ansi-white-bg {
  background-color: #C5C1B4;
}
.ansi-white-intense-fg {
  color: #A1A6B2;
}
.ansi-white-intense-bg {
  background-color: #A1A6B2;
}
.ansi-default-inverse-fg {
  color: #FFFFFF;
}
.ansi-default-inverse-bg {
  background-color: #000000;
}
.ansi-bold {
  font-weight: bold;
}
.ansi-underline {
  text-decoration: underline;
}
/* The following styles are deprecated an will be removed in a future version */
.ansibold {
  font-weight: bold;
}
.ansi-inverse {
  outline: 0.5px dotted;
}
/* use dark versions for foreground, to improve visibility */
.ansiblack {
  color: black;
}
.ansired {
  color: darkred;
}
.ansigreen {
  color: darkgreen;
}
.ansiyellow {
  color: #c4a000;
}
.ansiblue {
  color: darkblue;
}
.ansipurple {
  color: darkviolet;
}
.ansicyan {
  color: steelblue;
}
.ansigray {
  color: gray;
}
/* and light for background, for the same reason */
.ansibgblack {
  background-color: black;
}
.ansibgred {
  background-color: red;
}
.ansibggreen {
  background-color: green;
}
.ansibgyellow {
  background-color: yellow;
}
.ansibgblue {
  background-color: blue;
}
.ansibgpurple {
  background-color: magenta;
}
.ansibgcyan {
  background-color: cyan;
}
.ansibggray {
  background-color: gray;
}
div.cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-radius: 2px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: transparent;
  width: 100%;
  padding: 5px;
  /* This acts as a spacer between cells, that is outside the border */
  margin: 0px;
  outline: none;
  position: relative;
  overflow: visible;
}
div.cell:before {
  position: absolute;
  display: block;
  top: -1px;
  left: -1px;
  width: 5px;
  height: calc(100% +  2px);
  content: '';
  background: transparent;
}
div.cell.jupyter-soft-selected {
  border-left-color: #E3F2FD;
  border-left-width: 1px;
  padding-left: 5px;
  border-right-color: #E3F2FD;
  border-right-width: 1px;
  background: #E3F2FD;
}
@media print {
  div.cell.jupyter-soft-selected {
    border-color: transparent;
  }
}
div.cell.selected,
div.cell.selected.jupyter-soft-selected {
  border-color: #ababab;
}
div.cell.selected:before,
div.cell.selected.jupyter-soft-selected:before {
  position: absolute;
  display: block;
  top: -1px;
  left: -1px;
  width: 5px;
  height: calc(100% +  2px);
  content: '';
  background: #42A5F5;
}
@media print {
  div.cell.selected,
  div.cell.selected.jupyter-soft-selected {
    border-color: transparent;
  }
}
.edit_mode div.cell.selected {
  border-color: #66BB6A;
}
.edit_mode div.cell.selected:before {
  position: absolute;
  display: block;
  top: -1px;
  left: -1px;
  width: 5px;
  height: calc(100% +  2px);
  content: '';
  background: #66BB6A;
}
@media print {
  .edit_mode div.cell.selected {
    border-color: transparent;
  }
}
.prompt {
  /* This needs to be wide enough for 3 digit prompt numbers: In[100]: */
  min-width: 14ex;
  /* This padding is tuned to match the padding on the CodeMirror editor. */
  padding: 0.4em;
  margin: 0px;
  font-family: monospace;
  text-align: right;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
  /* Don't highlight prompt number selection */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  /* Use default cursor */
  cursor: default;
}
@media (max-width: 540px) {
  .prompt {
    text-align: left;
  }
}
div.inner_cell {
  min-width: 0;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_area {
  border: 1px solid #cfcfcf;
  border-radius: 2px;
  background: #f7f7f7;
  line-height: 1.21429em;
}
/* This is needed so that empty prompt areas can collapse to zero height when there
   is no content in the output_subarea and the prompt. The main purpose of this is
   to make sure that empty JavaScript output_subareas have no height. */
div.prompt:empty {
  padding-top: 0;
  padding-bottom: 0;
}
div.unrecognized_cell {
  padding: 5px 5px 5px 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.unrecognized_cell .inner_cell {
  border-radius: 2px;
  padding: 5px;
  font-weight: bold;
  color: red;
  border: 1px solid #cfcfcf;
  background: #eaeaea;
}
div.unrecognized_cell .inner_cell a {
  color: inherit;
  text-decoration: none;
}
div.unrecognized_cell .inner_cell a:hover {
  color: inherit;
  text-decoration: none;
}
@media (max-width: 540px) {
  div.unrecognized_cell > div.prompt {
    display: none;
  }
}
div.code_cell {
  /* avoid page breaking on code cells when printing */
}
@media print {
  div.code_cell {
    page-break-inside: avoid;
  }
}
/* any special styling for code cells that are currently running goes here */
div.input {
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.input {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_prompt {
  color: #303F9F;
  border-top: 1px solid transparent;
}
div.input_area > div.highlight {
  margin: 0.4em;
  border: none;
  padding: 0px;
  background-color: transparent;
}
div.input_area > div.highlight > pre {
  margin: 0px;
  border: none;
  padding: 0px;
  background-color: transparent;
}
/* The following gets added to the <head> if it is detected that the user has a
 * monospace font with inconsistent normal/bold/italic height.  See
 * notebookmain.js.  Such fonts will have keywords vertically offset with
 * respect to the rest of the text.  The user should select a better font.
 * See: https://github.com/ipython/ipython/issues/1503
 *
 * .CodeMirror span {
 *      vertical-align: bottom;
 * }
 */
.CodeMirror {
  line-height: 1.21429em;
  /* Changed from 1em to our global default */
  font-size: 14px;
  height: auto;
  /* Changed to auto to autogrow */
  background: none;
  /* Changed from white to allow our bg to show through */
}
.CodeMirror-scroll {
  /*  The CodeMirror docs are a bit fuzzy on if overflow-y should be hidden or visible.*/
  /*  We have found that if it is visible, vertical scrollbars appear with font size changes.*/
  overflow-y: hidden;
  overflow-x: auto;
}
.CodeMirror-lines {
  /* In CM2, this used to be 0.4em, but in CM3 it went to 4px. We need the em value because */
  /* we have set a different line-height and want this to scale with that. */
  /* Note that this should set vertical padding only, since CodeMirror assumes
       that horizontal padding will be set on CodeMirror pre */
  padding: 0.4em 0;
}
.CodeMirror-linenumber {
  padding: 0 8px 0 4px;
}
.CodeMirror-gutters {
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.CodeMirror pre {
  /* In CM3 this went to 4px from 0 in CM2. This sets horizontal padding only,
    use .CodeMirror-lines for vertical */
  padding: 0 0.4em;
  border: 0;
  border-radius: 0;
}
.CodeMirror-cursor {
  border-left: 1.4px solid black;
}
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .CodeMirror-cursor {
    border-left: 2px solid black;
  }
}
@media screen and (min-width: 4320px) {
  .CodeMirror-cursor {
    border-left: 4px solid black;
  }
}
/*

Original style from softwaremaniacs.org (c) Ivan Sagalaev <Maniac@SoftwareManiacs.Org>
Adapted from GitHub theme

*/
.highlight-base {
  color: #000;
}
.highlight-variable {
  color: #000;
}
.highlight-variable-2 {
  color: #1a1a1a;
}
.highlight-variable-3 {
  color: #333333;
}
.highlight-string {
  color: #BA2121;
}
.highlight-comment {
  color: #408080;
  font-style: italic;
}
.highlight-number {
  color: #080;
}
.highlight-atom {
  color: #88F;
}
.highlight-keyword {
  color: #008000;
  font-weight: bold;
}
.highlight-builtin {
  color: #008000;
}
.highlight-error {
  color: #f00;
}
.highlight-operator {
  color: #AA22FF;
  font-weight: bold;
}
.highlight-meta {
  color: #AA22FF;
}
/* previously not defined, copying from default codemirror */
.highlight-def {
  color: #00f;
}
.highlight-string-2 {
  color: #f50;
}
.highlight-qualifier {
  color: #555;
}
.highlight-bracket {
  color: #997;
}
.highlight-tag {
  color: #170;
}
.highlight-attribute {
  color: #00c;
}
.highlight-header {
  color: blue;
}
.highlight-quote {
  color: #090;
}
.highlight-link {
  color: #00c;
}
/* apply the same style to codemirror */
.cm-s-ipython span.cm-keyword {
  color: #008000;
  font-weight: bold;
}
.cm-s-ipython span.cm-atom {
  color: #88F;
}
.cm-s-ipython span.cm-number {
  color: #080;
}
.cm-s-ipython span.cm-def {
  color: #00f;
}
.cm-s-ipython span.cm-variable {
  color: #000;
}
.cm-s-ipython span.cm-operator {
  color: #AA22FF;
  font-weight: bold;
}
.cm-s-ipython span.cm-variable-2 {
  color: #1a1a1a;
}
.cm-s-ipython span.cm-variable-3 {
  color: #333333;
}
.cm-s-ipython span.cm-comment {
  color: #408080;
  font-style: italic;
}
.cm-s-ipython span.cm-string {
  color: #BA2121;
}
.cm-s-ipython span.cm-string-2 {
  color: #f50;
}
.cm-s-ipython span.cm-meta {
  color: #AA22FF;
}
.cm-s-ipython span.cm-qualifier {
  color: #555;
}
.cm-s-ipython span.cm-builtin {
  color: #008000;
}
.cm-s-ipython span.cm-bracket {
  color: #997;
}
.cm-s-ipython span.cm-tag {
  color: #170;
}
.cm-s-ipython span.cm-attribute {
  color: #00c;
}
.cm-s-ipython span.cm-header {
  color: blue;
}
.cm-s-ipython span.cm-quote {
  color: #090;
}
.cm-s-ipython span.cm-link {
  color: #00c;
}
.cm-s-ipython span.cm-error {
  color: #f00;
}
.cm-s-ipython span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}
div.output_wrapper {
  /* this position must be relative to enable descendents to be absolute within it */
  position: relative;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  z-index: 1;
}
/* class for the output area when it should be height-limited */
div.output_scroll {
  /* ideally, this would be max-height, but FF barfs all over that */
  height: 24em;
  /* FF needs this *and the wrapper* to specify full width, or it will shrinkwrap */
  width: 100%;
  overflow: auto;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  display: block;
}
/* output div while it is collapsed */
div.output_collapsed {
  margin: 0px;
  padding: 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
div.out_prompt_overlay {
  height: 100%;
  padding: 0px 0.4em;
  position: absolute;
  border-radius: 2px;
}
div.out_prompt_overlay:hover {
  /* use inner shadow to get border that is computed the same on WebKit/FF */
  -webkit-box-shadow: inset 0 0 1px #000;
  box-shadow: inset 0 0 1px #000;
  background: rgba(240, 240, 240, 0.5);
}
div.output_prompt {
  color: #D84315;
}
/* This class is the outer container of all output sections. */
div.output_area {
  padding: 0px;
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.output_area .MathJax_Display {
  text-align: left !important;
}
div.output_area .rendered_html table {
  margin-left: 0;
  margin-right: 0;
}
div.output_area .rendered_html img {
  margin-left: 0;
  margin-right: 0;
}
div.output_area img,
div.output_area svg {
  max-width: 100%;
  height: auto;
}
div.output_area img.unconfined,
div.output_area svg.unconfined {
  max-width: none;
}
div.output_area .mglyph > img {
  max-width: none;
}
/* This is needed to protect the pre formating from global settings such
   as that of bootstrap */
.output {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.output_area {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
div.output_area pre {
  margin: 0;
  padding: 1px 0 1px 0;
  border: 0;
  vertical-align: baseline;
  color: black;
  background-color: transparent;
  border-radius: 0;
}
/* This class is for the output subarea inside the output_area and after
   the prompt div. */
div.output_subarea {
  overflow-x: auto;
  padding: 0.4em;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
  max-width: calc(100% - 14ex);
}
div.output_scroll div.output_subarea {
  overflow-x: visible;
}
/* The rest of the output_* classes are for special styling of the different
   output types */
/* all text output has this class: */
div.output_text {
  text-align: left;
  color: #000;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
}
/* stdout/stderr are 'text' as well as 'stream', but execute_result/error are *not* streams */
div.output_stderr {
  background: #fdd;
  /* very light red background for stderr */
}
div.output_latex {
  text-align: left;
}
/* Empty output_javascript divs should have no height */
div.output_javascript:empty {
  padding: 0;
}
.js-error {
  color: darkred;
}
/* raw_input styles */
div.raw_input_container {
  line-height: 1.21429em;
  padding-top: 5px;
}
pre.raw_input_prompt {
  /* nothing needed here. */
}
input.raw_input {
  font-family: monospace;
  font-size: inherit;
  color: inherit;
  width: auto;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
}
input.raw_input:focus {
  box-shadow: none;
}
p.p-space {
  margin-bottom: 10px;
}
div.output_unrecognized {
  padding: 5px;
  font-weight: bold;
  color: red;
}
div.output_unrecognized a {
  color: inherit;
  text-decoration: none;
}
div.output_unrecognized a:hover {
  color: inherit;
  text-decoration: none;
}
.rendered_html {
  color: #000;
  /* any extras will just be numbers: */
}
.rendered_html em {
  font-style: italic;
}
.rendered_html strong {
  font-weight: bold;
}
.rendered_html u {
  text-decoration: underline;
}
.rendered_html :link {
  text-decoration: underline;
}
.rendered_html :visited {
  text-decoration: underline;
}
.rendered_html h1 {
  font-size: 185.7%;
  margin: 1.08em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h2 {
  font-size: 157.1%;
  margin: 1.27em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h3 {
  font-size: 128.6%;
  margin: 1.55em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h4 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h5 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h6 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h1:first-child {
  margin-top: 0.538em;
}
.rendered_html h2:first-child {
  margin-top: 0.636em;
}
.rendered_html h3:first-child {
  margin-top: 0.777em;
}
.rendered_html h4:first-child {
  margin-top: 1em;
}
.rendered_html h5:first-child {
  margin-top: 1em;
}
.rendered_html h6:first-child {
  margin-top: 1em;
}
.rendered_html ul:not(.list-inline),
.rendered_html ol:not(.list-inline) {
  padding-left: 2em;
}
.rendered_html ul {
  list-style: disc;
}
.rendered_html ul ul {
  list-style: square;
  margin-top: 0;
}
.rendered_html ul ul ul {
  list-style: circle;
}
.rendered_html ol {
  list-style: decimal;
}
.rendered_html ol ol {
  list-style: upper-alpha;
  margin-top: 0;
}
.rendered_html ol ol ol {
  list-style: lower-alpha;
}
.rendered_html ol ol ol ol {
  list-style: lower-roman;
}
.rendered_html ol ol ol ol ol {
  list-style: decimal;
}
.rendered_html * + ul {
  margin-top: 1em;
}
.rendered_html * + ol {
  margin-top: 1em;
}
.rendered_html hr {
  color: black;
  background-color: black;
}
.rendered_html pre {
  margin: 1em 2em;
  padding: 0px;
  background-color: #fff;
}
.rendered_html code {
  background-color: #eff0f1;
}
.rendered_html p code {
  padding: 1px 5px;
}
.rendered_html pre code {
  background-color: #fff;
}
.rendered_html pre,
.rendered_html code {
  border: 0;
  color: #000;
  font-size: 100%;
}
.rendered_html blockquote {
  margin: 1em 2em;
}
.rendered_html table {
  margin-left: auto;
  margin-right: auto;
  border: none;
  border-collapse: collapse;
  border-spacing: 0;
  color: black;
  font-size: 12px;
  table-layout: fixed;
}
.rendered_html thead {
  border-bottom: 1px solid black;
  vertical-align: bottom;
}
.rendered_html tr,
.rendered_html th,
.rendered_html td {
  text-align: right;
  vertical-align: middle;
  padding: 0.5em 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}
.rendered_html th {
  font-weight: bold;
}
.rendered_html tbody tr:nth-child(odd) {
  background: #f5f5f5;
}
.rendered_html tbody tr:hover {
  background: rgba(66, 165, 245, 0.2);
}
.rendered_html * + table {
  margin-top: 1em;
}
.rendered_html p {
  text-align: left;
}
.rendered_html * + p {
  margin-top: 1em;
}
.rendered_html img {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.rendered_html * + img {
  margin-top: 1em;
}
.rendered_html img,
.rendered_html svg {
  max-width: 100%;
  height: auto;
}
.rendered_html img.unconfined,
.rendered_html svg.unconfined {
  max-width: none;
}
.rendered_html .alert {
  margin-bottom: initial;
}
.rendered_html * + .alert {
  margin-top: 1em;
}
[dir="rtl"] .rendered_html p {
  text-align: right;
}
div.text_cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.text_cell > div.prompt {
    display: none;
  }
}
div.text_cell_render {
  /*font-family: "Helvetica Neue", Arial, Helvetica, Geneva, sans-serif;*/
  outline: none;
  resize: none;
  width: inherit;
  border-style: none;
  padding: 0.5em 0.5em 0.5em 0.4em;
  color: #000;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
a.anchor-link:link {
  text-decoration: none;
  padding: 0px 20px;
  visibility: hidden;
}
h1:hover .anchor-link,
h2:hover .anchor-link,
h3:hover .anchor-link,
h4:hover .anchor-link,
h5:hover .anchor-link,
h6:hover .anchor-link {
  visibility: visible;
}
.text_cell.rendered .input_area {
  display: none;
}
.text_cell.rendered .rendered_html {
  overflow-x: auto;
  overflow-y: hidden;
}
.text_cell.rendered .rendered_html tr,
.text_cell.rendered .rendered_html th,
.text_cell.rendered .rendered_html td {
  max-width: none;
}
.text_cell.unrendered .text_cell_render {
  display: none;
}
.text_cell .dropzone .input_area {
  border: 2px dashed #bababa;
  margin: -1px;
}
.cm-header-1,
.cm-header-2,
.cm-header-3,
.cm-header-4,
.cm-header-5,
.cm-header-6 {
  font-weight: bold;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
.cm-header-1 {
  font-size: 185.7%;
}
.cm-header-2 {
  font-size: 157.1%;
}
.cm-header-3 {
  font-size: 128.6%;
}
.cm-header-4 {
  font-size: 110%;
}
.cm-header-5 {
  font-size: 100%;
  font-style: italic;
}
.cm-header-6 {
  font-size: 100%;
  font-style: italic;
}
/*!
*
* IPython notebook webapp
*
*/
@media (max-width: 767px) {
  .notebook_app {
    padding-left: 0px;
    padding-right: 0px;
  }
}
#ipython-main-app {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook_panel {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook {
  font-size: 14px;
  line-height: 20px;
  overflow-y: hidden;
  overflow-x: auto;
  width: 100%;
  /* This spaces the page away from the edge of the notebook area */
  padding-top: 20px;
  margin: 0px;
  outline: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  min-height: 100%;
}
@media not print {
  #notebook-container {
    padding: 15px;
    background-color: #fff;
    min-height: 0;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
@media print {
  #notebook-container {
    width: 100%;
  }
}
div.ui-widget-content {
  border: 1px solid #ababab;
  outline: none;
}
pre.dialog {
  background-color: #f7f7f7;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0.4em;
  padding-left: 2em;
}
p.dialog {
  padding: 0.2em;
}
/* Word-wrap output correctly.  This is the CSS3 spelling, though Firefox seems
   to not honor it correctly.  Webkit browsers (Chrome, rekonq, Safari) do.
 */
pre,
code,
kbd,
samp {
  white-space: pre-wrap;
}
#fonttest {
  font-family: monospace;
}
p {
  margin-bottom: 0;
}
.end_space {
  min-height: 100px;
  transition: height .2s ease;
}
.notebook_app > #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
@media not print {
  .notebook_app {
    background-color: #EEE;
  }
}
kbd {
  border-style: solid;
  border-width: 1px;
  box-shadow: none;
  margin: 2px;
  padding-left: 2px;
  padding-right: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
.jupyter-keybindings {
  padding: 1px;
  line-height: 24px;
  border-bottom: 1px solid gray;
}
.jupyter-keybindings input {
  margin: 0;
  padding: 0;
  border: none;
}
.jupyter-keybindings i {
  padding: 6px;
}
.well code {
  background-color: #ffffff;
  border-color: #ababab;
  border-width: 1px;
  border-style: solid;
  padding: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
/* CSS for the cell toolbar */
.celltoolbar {
  border: thin solid #CFCFCF;
  border-bottom: none;
  background: #EEE;
  border-radius: 2px 2px 0px 0px;
  width: 100%;
  height: 29px;
  padding-right: 4px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
  display: -webkit-flex;
}
@media print {
  .celltoolbar {
    display: none;
  }
}
.ctb_hideshow {
  display: none;
  vertical-align: bottom;
}
/* ctb_show is added to the ctb_hideshow div to show the cell toolbar.
   Cell toolbars are only shown when the ctb_global_show class is also set.
*/
.ctb_global_show .ctb_show.ctb_hideshow {
  display: block;
}
.ctb_global_show .ctb_show + .input_area,
.ctb_global_show .ctb_show + div.text_cell_input,
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border-top-right-radius: 0px;
  border-top-left-radius: 0px;
}
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border: 1px solid #cfcfcf;
}
.celltoolbar {
  font-size: 87%;
  padding-top: 3px;
}
.celltoolbar select {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  width: inherit;
  font-size: inherit;
  height: 22px;
  padding: 0px;
  display: inline-block;
}
.celltoolbar select:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.celltoolbar select::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.celltoolbar select:-ms-input-placeholder {
  color: #999;
}
.celltoolbar select::-webkit-input-placeholder {
  color: #999;
}
.celltoolbar select::-ms-expand {
  border: 0;
  background-color: transparent;
}
.celltoolbar select[disabled],
.celltoolbar select[readonly],
fieldset[disabled] .celltoolbar select {
  background-color: #eeeeee;
  opacity: 1;
}
.celltoolbar select[disabled],
fieldset[disabled] .celltoolbar select {
  cursor: not-allowed;
}
textarea.celltoolbar select {
  height: auto;
}
select.celltoolbar select {
  height: 30px;
  line-height: 30px;
}
textarea.celltoolbar select,
select[multiple].celltoolbar select {
  height: auto;
}
.celltoolbar label {
  margin-left: 5px;
  margin-right: 5px;
}
.tags_button_container {
  width: 100%;
  display: flex;
}
.tag-container {
  display: flex;
  flex-direction: row;
  flex-grow: 1;
  overflow: hidden;
  position: relative;
}
.tag-container > * {
  margin: 0 4px;
}
.remove-tag-btn {
  margin-left: 4px;
}
.tags-input {
  display: flex;
}
.cell-tag:last-child:after {
  content: "";
  position: absolute;
  right: 0;
  width: 40px;
  height: 100%;
  /* Fade to background color of cell toolbar */
  background: linear-gradient(to right, rgba(0, 0, 0, 0), #EEE);
}
.tags-input > * {
  margin-left: 4px;
}
.cell-tag,
.tags-input input,
.tags-input button {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  box-shadow: none;
  width: inherit;
  font-size: inherit;
  height: 22px;
  line-height: 22px;
  padding: 0px 4px;
  display: inline-block;
}
.cell-tag:focus,
.tags-input input:focus,
.tags-input button:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.cell-tag::-moz-placeholder,
.tags-input input::-moz-placeholder,
.tags-input button::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.cell-tag:-ms-input-placeholder,
.tags-input input:-ms-input-placeholder,
.tags-input button:-ms-input-placeholder {
  color: #999;
}
.cell-tag::-webkit-input-placeholder,
.tags-input input::-webkit-input-placeholder,
.tags-input button::-webkit-input-placeholder {
  color: #999;
}
.cell-tag::-ms-expand,
.tags-input input::-ms-expand,
.tags-input button::-ms-expand {
  border: 0;
  background-color: transparent;
}
.cell-tag[disabled],
.tags-input input[disabled],
.tags-input button[disabled],
.cell-tag[readonly],
.tags-input input[readonly],
.tags-input button[readonly],
fieldset[disabled] .cell-tag,
fieldset[disabled] .tags-input input,
fieldset[disabled] .tags-input button {
  background-color: #eeeeee;
  opacity: 1;
}
.cell-tag[disabled],
.tags-input input[disabled],
.tags-input button[disabled],
fieldset[disabled] .cell-tag,
fieldset[disabled] .tags-input input,
fieldset[disabled] .tags-input button {
  cursor: not-allowed;
}
textarea.cell-tag,
textarea.tags-input input,
textarea.tags-input button {
  height: auto;
}
select.cell-tag,
select.tags-input input,
select.tags-input button {
  height: 30px;
  line-height: 30px;
}
textarea.cell-tag,
textarea.tags-input input,
textarea.tags-input button,
select[multiple].cell-tag,
select[multiple].tags-input input,
select[multiple].tags-input button {
  height: auto;
}
.cell-tag,
.tags-input button {
  padding: 0px 4px;
}
.cell-tag {
  background-color: #fff;
  white-space: nowrap;
}
.tags-input input[type=text]:focus {
  outline: none;
  box-shadow: none;
  border-color: #ccc;
}
.completions {
  position: absolute;
  z-index: 110;
  overflow: hidden;
  border: 1px solid #ababab;
  border-radius: 2px;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  line-height: 1;
}
.completions select {
  background: white;
  outline: none;
  border: none;
  padding: 0px;
  margin: 0px;
  overflow: auto;
  font-family: monospace;
  font-size: 110%;
  color: #000;
  width: auto;
}
.completions select option.context {
  color: #286090;
}
#kernel_logo_widget .current_kernel_logo {
  display: none;
  margin-top: -1px;
  margin-bottom: -1px;
  width: 32px;
  height: 32px;
}
[dir="rtl"] #kernel_logo_widget {
  float: left !important;
  float: left;
}
.modal .modal-body .move-path {
  display: flex;
  flex-direction: row;
  justify-content: space;
  align-items: center;
}
.modal .modal-body .move-path .server-root {
  padding-right: 20px;
}
.modal .modal-body .move-path .path-input {
  flex: 1;
}
#menubar {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  margin-top: 1px;
}
#menubar .navbar {
  border-top: 1px;
  border-radius: 0px 0px 2px 2px;
  margin-bottom: 0px;
}
#menubar .navbar-toggle {
  float: left;
  padding-top: 7px;
  padding-bottom: 7px;
  border: none;
}
#menubar .navbar-collapse {
  clear: left;
}
[dir="rtl"] #menubar .navbar-toggle {
  float: right;
}
[dir="rtl"] #menubar .navbar-collapse {
  clear: right;
}
[dir="rtl"] #menubar .navbar-nav {
  float: right;
}
[dir="rtl"] #menubar .nav {
  padding-right: 0px;
}
[dir="rtl"] #menubar .navbar-nav > li {
  float: right;
}
[dir="rtl"] #menubar .navbar-right {
  float: left !important;
}
[dir="rtl"] ul.dropdown-menu {
  text-align: right;
  left: auto;
}
[dir="rtl"] ul#new-menu.dropdown-menu {
  right: auto;
  left: 0;
}
.nav-wrapper {
  border-bottom: 1px solid #e7e7e7;
}
i.menu-icon {
  padding-top: 4px;
}
[dir="rtl"] i.menu-icon.pull-right {
  float: left !important;
  float: left;
}
ul#help_menu li a {
  overflow: hidden;
  padding-right: 2.2em;
}
ul#help_menu li a i {
  margin-right: -1.2em;
}
[dir="rtl"] ul#help_menu li a {
  padding-left: 2.2em;
}
[dir="rtl"] ul#help_menu li a i {
  margin-right: 0;
  margin-left: -1.2em;
}
[dir="rtl"] ul#help_menu li a i.pull-right {
  float: left !important;
  float: left;
}
.dropdown-submenu {
  position: relative;
}
.dropdown-submenu > .dropdown-menu {
  top: 0;
  left: 100%;
  margin-top: -6px;
  margin-left: -1px;
}
[dir="rtl"] .dropdown-submenu > .dropdown-menu {
  right: 100%;
  margin-right: -1px;
}
.dropdown-submenu:hover > .dropdown-menu {
  display: block;
}
.dropdown-submenu > a:after {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: block;
  content: "\f0da";
  float: right;
  color: #333333;
  margin-top: 2px;
  margin-right: -10px;
}
.dropdown-submenu > a:after.fa-pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.fa-pull-right {
  margin-left: .3em;
}
.dropdown-submenu > a:after.pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.pull-right {
  margin-left: .3em;
}
[dir="rtl"] .dropdown-submenu > a:after {
  float: left;
  content: "\f0d9";
  margin-right: 0;
  margin-left: -10px;
}
.dropdown-submenu:hover > a:after {
  color: #262626;
}
.dropdown-submenu.pull-left {
  float: none;
}
.dropdown-submenu.pull-left > .dropdown-menu {
  left: -100%;
  margin-left: 10px;
}
#notification_area {
  float: right !important;
  float: right;
  z-index: 10;
}
[dir="rtl"] #notification_area {
  float: left !important;
  float: left;
}
.indicator_area {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
[dir="rtl"] .indicator_area {
  float: left !important;
  float: left;
}
#kernel_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  border-left: 1px solid;
}
#kernel_indicator .kernel_indicator_name {
  padding-left: 5px;
  padding-right: 5px;
}
[dir="rtl"] #kernel_indicator {
  float: left !important;
  float: left;
  border-left: 0;
  border-right: 1px solid;
}
#modal_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
[dir="rtl"] #modal_indicator {
  float: left !important;
  float: left;
}
#readonly-indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  margin-top: 2px;
  margin-bottom: 0px;
  margin-left: 0px;
  margin-right: 0px;
  display: none;
}
.modal_indicator:before {
  width: 1.28571429em;
  text-align: center;
}
.edit_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f040";
}
.edit_mode .modal_indicator:before.fa-pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.fa-pull-right {
  margin-left: .3em;
}
.edit_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: ' ';
}
.command_mode .modal_indicator:before.fa-pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.fa-pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f10c";
}
.kernel_idle_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f111";
}
.kernel_busy_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f1e2";
}
.kernel_dead_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f127";
}
.kernel_disconnected_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.pull-right {
  margin-left: .3em;
}
.notification_widget {
  color: #777;
  z-index: 10;
  background: rgba(240, 240, 240, 0.5);
  margin-right: 4px;
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget:focus,
.notification_widget.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.notification_widget:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active:hover,
.notification_widget.active:hover,
.open > .dropdown-toggle.notification_widget:hover,
.notification_widget:active:focus,
.notification_widget.active:focus,
.open > .dropdown-toggle.notification_widget:focus,
.notification_widget:active.focus,
.notification_widget.active.focus,
.open > .dropdown-toggle.notification_widget.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  background-image: none;
}
.notification_widget.disabled:hover,
.notification_widget[disabled]:hover,
fieldset[disabled] .notification_widget:hover,
.notification_widget.disabled:focus,
.notification_widget[disabled]:focus,
fieldset[disabled] .notification_widget:focus,
.notification_widget.disabled.focus,
.notification_widget[disabled].focus,
fieldset[disabled] .notification_widget.focus {
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget .badge {
  color: #fff;
  background-color: #333;
}
.notification_widget.warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning:focus,
.notification_widget.warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.notification_widget.warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active:hover,
.notification_widget.warning.active:hover,
.open > .dropdown-toggle.notification_widget.warning:hover,
.notification_widget.warning:active:focus,
.notification_widget.warning.active:focus,
.open > .dropdown-toggle.notification_widget.warning:focus,
.notification_widget.warning:active.focus,
.notification_widget.warning.active.focus,
.open > .dropdown-toggle.notification_widget.warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  background-image: none;
}
.notification_widget.warning.disabled:hover,
.notification_widget.warning[disabled]:hover,
fieldset[disabled] .notification_widget.warning:hover,
.notification_widget.warning.disabled:focus,
.notification_widget.warning[disabled]:focus,
fieldset[disabled] .notification_widget.warning:focus,
.notification_widget.warning.disabled.focus,
.notification_widget.warning[disabled].focus,
fieldset[disabled] .notification_widget.warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.notification_widget.success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success:focus,
.notification_widget.success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.notification_widget.success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active:hover,
.notification_widget.success.active:hover,
.open > .dropdown-toggle.notification_widget.success:hover,
.notification_widget.success:active:focus,
.notification_widget.success.active:focus,
.open > .dropdown-toggle.notification_widget.success:focus,
.notification_widget.success:active.focus,
.notification_widget.success.active.focus,
.open > .dropdown-toggle.notification_widget.success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  background-image: none;
}
.notification_widget.success.disabled:hover,
.notification_widget.success[disabled]:hover,
fieldset[disabled] .notification_widget.success:hover,
.notification_widget.success.disabled:focus,
.notification_widget.success[disabled]:focus,
fieldset[disabled] .notification_widget.success:focus,
.notification_widget.success.disabled.focus,
.notification_widget.success[disabled].focus,
fieldset[disabled] .notification_widget.success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.notification_widget.info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info:focus,
.notification_widget.info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.notification_widget.info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active:hover,
.notification_widget.info.active:hover,
.open > .dropdown-toggle.notification_widget.info:hover,
.notification_widget.info:active:focus,
.notification_widget.info.active:focus,
.open > .dropdown-toggle.notification_widget.info:focus,
.notification_widget.info:active.focus,
.notification_widget.info.active.focus,
.open > .dropdown-toggle.notification_widget.info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  background-image: none;
}
.notification_widget.info.disabled:hover,
.notification_widget.info[disabled]:hover,
fieldset[disabled] .notification_widget.info:hover,
.notification_widget.info.disabled:focus,
.notification_widget.info[disabled]:focus,
fieldset[disabled] .notification_widget.info:focus,
.notification_widget.info.disabled.focus,
.notification_widget.info[disabled].focus,
fieldset[disabled] .notification_widget.info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.notification_widget.danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger:focus,
.notification_widget.danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.notification_widget.danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active:hover,
.notification_widget.danger.active:hover,
.open > .dropdown-toggle.notification_widget.danger:hover,
.notification_widget.danger:active:focus,
.notification_widget.danger.active:focus,
.open > .dropdown-toggle.notification_widget.danger:focus,
.notification_widget.danger:active.focus,
.notification_widget.danger.active.focus,
.open > .dropdown-toggle.notification_widget.danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  background-image: none;
}
.notification_widget.danger.disabled:hover,
.notification_widget.danger[disabled]:hover,
fieldset[disabled] .notification_widget.danger:hover,
.notification_widget.danger.disabled:focus,
.notification_widget.danger[disabled]:focus,
fieldset[disabled] .notification_widget.danger:focus,
.notification_widget.danger.disabled.focus,
.notification_widget.danger[disabled].focus,
fieldset[disabled] .notification_widget.danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger .badge {
  color: #d9534f;
  background-color: #fff;
}
div#pager {
  background-color: #fff;
  font-size: 14px;
  line-height: 20px;
  overflow: hidden;
  display: none;
  position: fixed;
  bottom: 0px;
  width: 100%;
  max-height: 50%;
  padding-top: 8px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  /* Display over codemirror */
  z-index: 100;
  /* Hack which prevents jquery ui resizable from changing top. */
  top: auto !important;
}
div#pager pre {
  line-height: 1.21429em;
  color: #000;
  background-color: #f7f7f7;
  padding: 0.4em;
}
div#pager #pager-button-area {
  position: absolute;
  top: 8px;
  right: 20px;
}
div#pager #pager-contents {
  position: relative;
  overflow: auto;
  width: 100%;
  height: 100%;
}
div#pager #pager-contents #pager-container {
  position: relative;
  padding: 15px 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
div#pager .ui-resizable-handle {
  top: 0px;
  height: 8px;
  background: #f7f7f7;
  border-top: 1px solid #cfcfcf;
  border-bottom: 1px solid #cfcfcf;
  /* This injects handle bars (a short, wide = symbol) for 
        the resize handle. */
}
div#pager .ui-resizable-handle::after {
  content: '';
  top: 2px;
  left: 50%;
  height: 3px;
  width: 30px;
  margin-left: -15px;
  position: absolute;
  border-top: 1px solid #cfcfcf;
}
.quickhelp {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  line-height: 1.8em;
}
.shortcut_key {
  display: inline-block;
  width: 21ex;
  text-align: right;
  font-family: monospace;
}
.shortcut_descr {
  display: inline-block;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
span.save_widget {
  height: 30px;
  margin-top: 4px;
  display: flex;
  justify-content: flex-start;
  align-items: baseline;
  width: 50%;
  flex: 1;
}
span.save_widget span.filename {
  height: 100%;
  line-height: 1em;
  margin-left: 16px;
  border: none;
  font-size: 146.5%;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
  border-radius: 2px;
}
span.save_widget span.filename:hover {
  background-color: #e6e6e6;
}
[dir="rtl"] span.save_widget.pull-left {
  float: right !important;
  float: right;
}
[dir="rtl"] span.save_widget span.filename {
  margin-left: 0;
  margin-right: 16px;
}
span.checkpoint_status,
span.autosave_status {
  font-size: small;
  white-space: nowrap;
  padding: 0 5px;
}
@media (max-width: 767px) {
  span.save_widget {
    font-size: small;
    padding: 0 0 0 5px;
  }
  span.checkpoint_status,
  span.autosave_status {
    display: none;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  span.checkpoint_status {
    display: none;
  }
  span.autosave_status {
    font-size: x-small;
  }
}
.toolbar {
  padding: 0px;
  margin-left: -5px;
  margin-top: 2px;
  margin-bottom: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.toolbar select,
.toolbar label {
  width: auto;
  vertical-align: middle;
  margin-right: 2px;
  margin-bottom: 0px;
  display: inline;
  font-size: 92%;
  margin-left: 0.3em;
  margin-right: 0.3em;
  padding: 0px;
  padding-top: 3px;
}
.toolbar .btn {
  padding: 2px 8px;
}
.toolbar .btn-group {
  margin-top: 0px;
  margin-left: 5px;
}
.toolbar-btn-label {
  margin-left: 6px;
}
#maintoolbar {
  margin-bottom: -3px;
  margin-top: -8px;
  border: 0px;
  min-height: 27px;
  margin-left: 0px;
  padding-top: 11px;
  padding-bottom: 3px;
}
#maintoolbar .navbar-text {
  float: none;
  vertical-align: middle;
  text-align: right;
  margin-left: 5px;
  margin-right: 0px;
  margin-top: 0px;
}
.select-xs {
  height: 24px;
}
[dir="rtl"] .btn-group > .btn,
.btn-group-vertical > .btn {
  float: right;
}
.pulse,
.dropdown-menu > li > a.pulse,
li.pulse > a.dropdown-toggle,
li.pulse.open > a.dropdown-toggle {
  background-color: #F37626;
  color: white;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
/** WARNING IF YOU ARE EDITTING THIS FILE, if this is a .css file, It has a lot
 * of chance of beeing generated from the ../less/[samename].less file, you can
 * try to get back the less file by reverting somme commit in history
 **/
/*
 * We'll try to get something pretty, so we
 * have some strange css to have the scroll bar on
 * the left with fix button on the top right of the tooltip
 */
@-moz-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-webkit-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-moz-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
/*properties of tooltip after "expand"*/
.bigtooltip {
  overflow: auto;
  height: 200px;
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
}
/*properties of tooltip before "expand"*/
.smalltooltip {
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
  text-overflow: ellipsis;
  overflow: hidden;
  height: 80px;
}
.tooltipbuttons {
  position: absolute;
  padding-right: 15px;
  top: 0px;
  right: 0px;
}
.tooltiptext {
  /*avoid the button to overlap on some docstring*/
  padding-right: 30px;
}
.ipython_tooltip {
  max-width: 700px;
  /*fade-in animation when inserted*/
  -webkit-animation: fadeOut 400ms;
  -moz-animation: fadeOut 400ms;
  animation: fadeOut 400ms;
  -webkit-animation: fadeIn 400ms;
  -moz-animation: fadeIn 400ms;
  animation: fadeIn 400ms;
  vertical-align: middle;
  background-color: #f7f7f7;
  overflow: visible;
  border: #ababab 1px solid;
  outline: none;
  padding: 3px;
  margin: 0px;
  padding-left: 7px;
  font-family: monospace;
  min-height: 50px;
  -moz-box-shadow: 0px 6px 10px -1px #adadad;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  border-radius: 2px;
  position: absolute;
  z-index: 1000;
}
.ipython_tooltip a {
  float: right;
}
.ipython_tooltip .tooltiptext pre {
  border: 0;
  border-radius: 0;
  font-size: 100%;
  background-color: #f7f7f7;
}
.pretooltiparrow {
  left: 0px;
  margin: 0px;
  top: -16px;
  width: 40px;
  height: 16px;
  overflow: hidden;
  position: absolute;
}
.pretooltiparrow:before {
  background-color: #f7f7f7;
  border: 1px #ababab solid;
  z-index: 11;
  content: "";
  position: absolute;
  left: 15px;
  top: 10px;
  width: 25px;
  height: 25px;
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  -o-transform: rotate(45deg);
}
ul.typeahead-list i {
  margin-left: -10px;
  width: 18px;
}
[dir="rtl"] ul.typeahead-list i {
  margin-left: 0;
  margin-right: -10px;
}
ul.typeahead-list {
  max-height: 80vh;
  overflow: auto;
}
ul.typeahead-list > li > a {
  /** Firefox bug **/
  /* see https://github.com/jupyter/notebook/issues/559 */
  white-space: normal;
}
ul.typeahead-list  > li > a.pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .typeahead-list {
  text-align: right;
}
.cmd-palette .modal-body {
  padding: 7px;
}
.cmd-palette form {
  background: white;
}
.cmd-palette input {
  outline: none;
}
.no-shortcut {
  min-width: 20px;
  color: transparent;
}
[dir="rtl"] .no-shortcut.pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .command-shortcut.pull-right {
  float: left !important;
  float: left;
}
.command-shortcut:before {
  content: "(command mode)";
  padding-right: 3px;
  color: #777777;
}
.edit-shortcut:before {
  content: "(edit)";
  padding-right: 3px;
  color: #777777;
}
[dir="rtl"] .edit-shortcut.pull-right {
  float: left !important;
  float: left;
}
#find-and-replace #replace-preview .match,
#find-and-replace #replace-preview .insert {
  background-color: #BBDEFB;
  border-color: #90CAF9;
  border-style: solid;
  border-width: 1px;
  border-radius: 0px;
}
[dir="ltr"] #find-and-replace .input-group-btn + .form-control {
  border-left: none;
}
[dir="rtl"] #find-and-replace .input-group-btn + .form-control {
  border-right: none;
}
#find-and-replace #replace-preview .replace .match {
  background-color: #FFCDD2;
  border-color: #EF9A9A;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .insert {
  background-color: #C8E6C9;
  border-color: #A5D6A7;
  border-radius: 0px;
}
#find-and-replace #replace-preview {
  max-height: 60vh;
  overflow: auto;
}
#find-and-replace #replace-preview pre {
  padding: 5px 10px;
}
.terminal-app {
  background: #EEE;
}
.terminal-app #header {
  background: #fff;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.terminal-app .terminal {
  width: 100%;
  float: left;
  font-family: monospace;
  color: white;
  background: black;
  padding: 0.4em;
  border-radius: 2px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
}
.terminal-app .terminal,
.terminal-app .terminal dummy-screen {
  line-height: 1em;
  font-size: 14px;
}
.terminal-app .terminal .xterm-rows {
  padding: 10px;
}
.terminal-app .terminal-cursor {
  color: black;
  background: white;
}
.terminal-app #terminado-container {
  margin-top: 20px;
}
/*# sourceMappingURL=style.min.css.map */
    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .ch { color: #408080; font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .cpf { color: #408080; font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sa { color: #BA2121 } /* Literal.String.Affix */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .dl { color: #BA2121 } /* Literal.String.Delimiter */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .fm { color: #0000FF } /* Name.Function.Magic */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .vm { color: #19177C } /* Name.Variable.Magic */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>
<style type="text/css">
    
/* Temporary definitions which will become obsolete with Notebook release 5.0 */
.ansi-black-fg { color: #3E424D; }
.ansi-black-bg { background-color: #3E424D; }
.ansi-black-intense-fg { color: #282C36; }
.ansi-black-intense-bg { background-color: #282C36; }
.ansi-red-fg { color: #E75C58; }
.ansi-red-bg { background-color: #E75C58; }
.ansi-red-intense-fg { color: #B22B31; }
.ansi-red-intense-bg { background-color: #B22B31; }
.ansi-green-fg { color: #00A250; }
.ansi-green-bg { background-color: #00A250; }
.ansi-green-intense-fg { color: #007427; }
.ansi-green-intense-bg { background-color: #007427; }
.ansi-yellow-fg { color: #DDB62B; }
.ansi-yellow-bg { background-color: #DDB62B; }
.ansi-yellow-intense-fg { color: #B27D12; }
.ansi-yellow-intense-bg { background-color: #B27D12; }
.ansi-blue-fg { color: #208FFB; }
.ansi-blue-bg { background-color: #208FFB; }
.ansi-blue-intense-fg { color: #0065CA; }
.ansi-blue-intense-bg { background-color: #0065CA; }
.ansi-magenta-fg { color: #D160C4; }
.ansi-magenta-bg { background-color: #D160C4; }
.ansi-magenta-intense-fg { color: #A03196; }
.ansi-magenta-intense-bg { background-color: #A03196; }
.ansi-cyan-fg { color: #60C6C8; }
.ansi-cyan-bg { background-color: #60C6C8; }
.ansi-cyan-intense-fg { color: #258F8F; }
.ansi-cyan-intense-bg { background-color: #258F8F; }
.ansi-white-fg { color: #C5C1B4; }
.ansi-white-bg { background-color: #C5C1B4; }
.ansi-white-intense-fg { color: #A1A6B2; }
.ansi-white-intense-bg { background-color: #A1A6B2; }

.ansi-bold { font-weight: bold; }

    </style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  } 
  div.output_wrapper { 
    display: block;
    page-break-inside: avoid; 
  }
  div.output { 
    display: block;
    page-break-inside: avoid; 
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<link rel="stylesheet" href="custom.css">

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Weighted-graph-theory-measures-on-numpy-arrays.">Weighted graph theory measures on numpy arrays.<a class="anchor-link" href="#Weighted-graph-theory-measures-on-numpy-arrays.">&#182;</a></h1><p>This ipynb file aims to define different "small-worldness" measures (and other relevant weighted graph measures) for simple numpy array data containers,
in which a numpy array of shape (n_nodes, n_nodes) depicts a weighted network matrix. Hereby the value of matrix[i, j] stands for the strength of the connection (i.e. the weight) between node i and node j.</p>
<p>This code is written in order to analyze brain connectivity data, as for example created by a connectivity measure between different EEG signals. This code especially aims to be easily applicable to <a href="https://github.com/mne-tools/mne-python">MNE-Python</a> data structures.</p>
<p>This code was created to use for a student study project at the University of Osnabrück and aims to provide a simple and computationally efficient alternative to the <a href="https://networkx.org">networkx graph toolbox</a>. Most of these functions are derived from Rubinov &amp; Sporns (2010). If you're interested in these implementations, you may also want to have a look at <a href="https://pypi.org/project/bctpy">bctpy</a> which is a Python graph theory toolbox that aims to replicate Sporns &amp; Rubinov's brain connectivity toolbox written for MATLAB.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>We start with importing the neccessary stuff:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[44]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Data-generation">Data generation<a class="anchor-link" href="#Data-generation">&#182;</a></h2><p>First, we need to generate a fake connectivity matrix / graph. Since we want to compare this graph against random graphs later, we can not simply generate a random matrix, but generate a non-random one.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[45]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">generate_graph</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">,</span> <span class="n">regularity</span><span class="o">=</span><span class="mf">0.1</span><span class="p">):</span>
  <span class="c1"># start with a random matrix</span>
  <span class="n">matrix</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">rand</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">,</span> <span class="n">n_nodes</span><span class="p">)</span>

  <span class="c1"># make funny patterns:</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
    <span class="k">for</span> <span class="n">ii</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
      <span class="k">if</span> <span class="n">matrix</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">ii</span><span class="p">]</span> <span class="o">&gt;</span> <span class="n">matrix</span><span class="p">[</span><span class="n">i</span> <span class="o">-</span> <span class="mi">3</span><span class="p">,</span> <span class="n">ii</span> <span class="o">-</span> <span class="mi">13</span><span class="p">]:</span>
        <span class="n">matrix</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">2</span><span class="p">:</span><span class="n">i</span><span class="o">+</span><span class="mi">2</span><span class="p">,</span> <span class="n">ii</span><span class="o">-</span><span class="mi">2</span><span class="p">:</span><span class="n">ii</span><span class="o">+</span><span class="mi">2</span><span class="p">]</span> <span class="o">+=</span> <span class="n">regularity</span>

  <span class="c1"># normalize it from 0 to 0.95, as we shouldn&#39;t assume that independet signals are perfectly connected.</span>
  <span class="n">matrix</span> <span class="o">/=</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span> <span class="o">/</span> <span class="mf">0.95</span>

  <span class="c1"># make it look like a connectivity matrix</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
    <span class="k">for</span> <span class="n">ii</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
      <span class="c1"># mirror it</span>
      <span class="n">matrix</span><span class="p">[</span><span class="n">ii</span><span class="p">,</span> <span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">matrix</span><span class="p">[</span><span class="n">i</span><span class="p">,</span><span class="n">ii</span><span class="p">]</span>

  <span class="n">matrix</span> <span class="o">=</span> <span class="n">remove_self_connections</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>

  <span class="k">return</span> <span class="n">matrix</span> <span class="c1"># 1 - matrix!</span>


<span class="k">def</span> <span class="nf">remove_self_connections</span><span class="p">(</span><span class="n">matrix</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Removes the self-connections of a network graph.&quot;&quot;&quot;</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">matrix</span><span class="p">)):</span>
    <span class="n">matrix</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="mi">0</span>
  <span class="k">return</span> <span class="n">matrix</span>


<span class="k">def</span> <span class="nf">invert_matrix</span><span class="p">(</span><span class="n">matrix</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Invert a matrix from 0 to 1, dependent on whether dealing with distances or weight strengths.&quot;&quot;&quot;</span>
  <span class="n">new_matrix</span> <span class="o">=</span> <span class="mi">1</span> <span class="o">-</span> <span class="n">matrix</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
  <span class="k">return</span> <span class="n">remove_self_connections</span><span class="p">(</span><span class="n">new_matrix</span><span class="p">)</span>


<span class="k">def</span> <span class="nf">plot_graph</span><span class="p">(</span><span class="n">graph_matrix</span><span class="p">,</span> <span class="n">title</span><span class="o">=</span><span class="s2">&quot;Connectivity/Graph Matrix&quot;</span><span class="p">,</span> <span class="n">show</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">cb</span><span class="o">=</span><span class="kc">True</span><span class="p">):</span>
  <span class="n">plt</span><span class="o">.</span><span class="n">pcolormesh</span><span class="p">(</span><span class="n">graph_matrix</span><span class="p">,</span> <span class="n">vmin</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span> <span class="n">vmax</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
  <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="n">title</span><span class="p">)</span>
  <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Channels/Nodes&#39;</span><span class="p">)</span>
  <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Channels/Nodes&#39;</span><span class="p">)</span>
  <span class="k">if</span> <span class="n">cb</span><span class="p">:</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">colorbar</span><span class="p">(</span><span class="n">ticks</span><span class="o">=</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="o">.</span><span class="mi">5</span><span class="p">,</span> <span class="mi">1</span><span class="p">])</span>
  <span class="k">if</span> <span class="n">show</span><span class="p">:</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
  

<span class="n">plot_graph</span><span class="p">(</span><span class="n">generate_graph</span><span class="p">(</span><span class="n">n_nodes</span><span class="o">=</span><span class="mi">25</span><span class="p">,</span> <span class="n">regularity</span><span class="o">=</span><span class="mf">0.05</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Define-the-graph-measures-needed-for-small-worldness">Define the graph measures needed for small worldness<a class="anchor-link" href="#Define-the-graph-measures-needed-for-small-worldness">&#182;</a></h2><p>If not stated otherwise, all formulas are taken from:</p>
<p>Rubinov &amp; Sporns (2010). Complex network measures of brain connectivity: Uses and interpretations</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[106]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">weighted_shortest_path</span><span class="p">(</span><span class="n">matrix</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">  Calculate the shortest path lengths between all nodes in a weighted graph.</span>

<span class="sd">  This is an implementation of the Floyd-Warshall algorithm for finding the shortest</span>
<span class="sd">  path lengths of an entire graph matrix. Implementation taken from:</span>
<span class="sd">  https://en.wikipedia.org/wiki/Floyd%E2%80%93Warshall_algorithm</span>

<span class="sd">  This implementation is actually identical to scipy.sparse.csgraph.floyd_warshall,</span>
<span class="sd">  which we found after the implementation.</span>
<span class="sd">  &quot;&quot;&quot;</span>
  <span class="n">matrix</span> <span class="o">=</span> <span class="n">invert_matrix</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>

  <span class="n">n_nodes</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
  <span class="n">distances</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">([</span><span class="n">n_nodes</span><span class="p">,</span> <span class="n">n_nodes</span><span class="p">])</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
      <span class="n">distances</span><span class="p">[</span><span class="n">i</span><span class="p">,</span><span class="n">j</span><span class="p">]</span> <span class="o">=</span> <span class="n">matrix</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">]</span>
  
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
    <span class="n">distances</span><span class="p">[</span><span class="n">i</span><span class="p">,</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="mi">0</span>

  <span class="k">for</span> <span class="n">k</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
      <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
        <span class="k">if</span> <span class="n">distances</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">]</span> <span class="o">&gt;</span> <span class="n">distances</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">k</span><span class="p">]</span> <span class="o">+</span> <span class="n">distances</span><span class="p">[</span><span class="n">k</span><span class="p">,</span> <span class="n">j</span><span class="p">]:</span>
          <span class="n">distances</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">]</span> <span class="o">=</span> <span class="n">distances</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">k</span><span class="p">]</span> <span class="o">+</span> <span class="n">distances</span><span class="p">[</span><span class="n">k</span><span class="p">,</span> <span class="n">j</span><span class="p">]</span>

  <span class="k">return</span> <span class="n">distances</span>


<span class="k">def</span> <span class="nf">weighted_characteristic_path_length</span><span class="p">(</span><span class="n">matrix</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Calculate the characteristic path length for weighted graphs.&quot;&quot;&quot;</span>
  <span class="n">n_nodes</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
  <span class="n">min_distances</span> <span class="o">=</span> <span class="n">weighted_shortest_path</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>

  <span class="n">sum_vector</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">)</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
    <span class="c1"># calculate the inner sum</span>
    <span class="n">sum_vector</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">1</span><span class="o">/</span><span class="p">(</span><span class="n">n_nodes</span><span class="o">-</span><span class="mi">1</span><span class="p">))</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">([</span><span class="n">min_distances</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">]</span> <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">)</span> <span class="k">if</span> <span class="n">j</span> <span class="o">!=</span> <span class="n">i</span><span class="p">])</span>

  <span class="k">return</span> <span class="p">(</span><span class="mi">1</span><span class="o">/</span><span class="n">n_nodes</span><span class="p">)</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">sum_vector</span><span class="p">)</span>


<span class="k">def</span> <span class="nf">weighted_node_degree</span><span class="p">(</span><span class="n">matrix</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Calculate the node degree for all nodes in a weighted graph.&quot;&quot;&quot;</span>
  <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">matrix</span><span class="p">,</span> <span class="n">axis</span><span class="o">=-</span><span class="mi">1</span><span class="p">)</span>


<span class="k">def</span> <span class="nf">unweighted_node_degree</span><span class="p">(</span><span class="n">matrix</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Calculate the node degree for all nodes in a weighted graph.&quot;&quot;&quot;</span>
  <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">ceil</span><span class="p">(</span><span class="n">matrix</span><span class="p">),</span> <span class="n">axis</span><span class="o">=-</span><span class="mi">1</span><span class="p">)</span>


<span class="k">def</span> <span class="nf">weighted_triangle_number</span><span class="p">(</span><span class="n">matrix</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Calculate the weighted geometric mean of triangles around i for all nodes i in a weighted graph.&quot;&quot;&quot;</span>
  <span class="n">n_nodes</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>

  <span class="n">mean_vector</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">([</span><span class="n">n_nodes</span><span class="p">])</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
    <span class="n">triangles</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([[</span><span class="n">matrix</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">]</span> <span class="o">*</span> <span class="n">matrix</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">k</span><span class="p">]</span> <span class="o">*</span> <span class="n">matrix</span><span class="p">[</span><span class="n">j</span><span class="p">,</span> <span class="n">k</span><span class="p">]</span> <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">)]</span> <span class="k">for</span> <span class="n">k</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">)])</span><span class="o">**</span><span class="p">(</span><span class="mi">1</span><span class="o">/</span><span class="mi">3</span><span class="p">)</span>
    <span class="n">mean_vector</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">1</span><span class="o">/</span><span class="mi">2</span><span class="p">)</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">triangles</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span><span class="mi">1</span><span class="p">))</span>
  
  <span class="k">return</span> <span class="n">mean_vector</span>


<span class="k">def</span> <span class="nf">weighted_clustering_coeff</span><span class="p">(</span><span class="n">matrix</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Calculate the clustering coefficient for a weighted graph.&quot;&quot;&quot;</span>
  <span class="n">n</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
  <span class="n">t</span> <span class="o">=</span> <span class="n">weighted_triangle_number</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
  <span class="n">k</span> <span class="o">=</span> <span class="n">unweighted_node_degree</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span> <span class="c1"># here we use the !max possible weights as reference</span>
  <span class="k">return</span> <span class="p">(</span><span class="mi">1</span><span class="o">/</span><span class="n">n</span><span class="p">)</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">((</span><span class="mi">2</span> <span class="o">*</span> <span class="n">t</span><span class="p">)</span><span class="o">/</span><span class="p">(</span><span class="n">k</span> <span class="o">*</span> <span class="p">(</span><span class="n">k</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)))</span>


<span class="k">def</span> <span class="nf">weighted_clustering_coeff_z</span><span class="p">(</span><span class="n">matrix</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Zhang&#39;s CC is an alternative clustering coefficient which should work better for our case See Samaräki et al. (2008).&quot;&quot;&quot;</span>
  <span class="n">n_nodes</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
  <span class="n">ccs</span> <span class="o">=</span> <span class="p">[]</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
    <span class="n">upper</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">([[</span><span class="n">matrix</span><span class="p">[</span><span class="n">i</span><span class="p">,</span><span class="n">j</span><span class="p">]</span> <span class="o">*</span> <span class="n">matrix</span><span class="p">[</span><span class="n">j</span><span class="p">,</span><span class="n">k</span><span class="p">]</span> <span class="o">*</span> <span class="n">matrix</span><span class="p">[</span><span class="n">i</span><span class="p">,</span><span class="n">k</span><span class="p">]</span> <span class="k">for</span> <span class="n">k</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">)]</span> <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">)])</span>
    <span class="n">lower</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">([[</span><span class="n">matrix</span><span class="p">[</span><span class="n">i</span><span class="p">,</span><span class="n">j</span><span class="p">]</span> <span class="o">*</span> <span class="n">matrix</span><span class="p">[</span><span class="n">i</span><span class="p">,</span><span class="n">k</span><span class="p">]</span> <span class="k">for</span> <span class="n">k</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">)</span> <span class="k">if</span> <span class="n">j</span><span class="o">!=</span><span class="n">k</span><span class="p">]</span> <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">)])</span>
    <span class="n">ccs</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">upper</span><span class="o">/</span><span class="n">lower</span><span class="p">)</span>

  <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">ccs</span><span class="p">)</span>
  

<span class="c1"># get an intuition for the shortest path length matrix</span>
<span class="n">matrix</span> <span class="o">=</span> <span class="n">generate_graph</span><span class="p">(</span><span class="n">n_nodes</span><span class="o">=</span><span class="mi">35</span><span class="p">,</span> <span class="n">regularity</span><span class="o">=</span><span class="mf">0.2</span><span class="p">)</span>
<span class="n">wsp</span> <span class="o">=</span> <span class="n">weighted_shortest_path</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>

<span class="n">plot_graph</span><span class="p">(</span><span class="n">matrix</span><span class="p">,</span> <span class="n">title</span><span class="o">=</span><span class="s2">&quot;Original graph matrix&quot;</span><span class="p">)</span>
<span class="n">plot_graph</span><span class="p">(</span><span class="n">wsp</span><span class="p">,</span> <span class="n">title</span><span class="o">=</span><span class="s2">&quot;Shortest path lengths between all nodes&quot;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Define-random/lattice-reference-shuffling-functions">Define random/lattice reference shuffling functions<a class="anchor-link" href="#Define-random/lattice-reference-shuffling-functions">&#182;</a></h2><p>When dealing with <em>complete</em> weighted graphs, we face certain problems when trying to calculate the small world coefficients: All small-world measures compare to random and lattice graphs which are created by shuffling the weights of the original graph. When trying to create a lattice reference graph, we use a markov procedure that allocates weights close to the main diagonal, resulting in a strictly ordered (=lattice) graph. However, usual lattice reference functions (e.g. the one used by networkx) only work for graphs that are not <em>complete</em>, i.e. not fully connected. They relocate only existing graph weights to previously non existing edges, which are closer to the diagonal than the original ones. However, when <em>all</em> nodes are connected this doesn't work. We adapted the original shuffling algorithm developed by Sporns &amp; Zwi (2004) and implemented in networkx such that <em>smaller</em> weights are relocated away from the diagonal, and <em>larger</em> weights are allocated towards the diagonal, arguing that smaller weights are closer to being non-existant than larger weights (which in our case of brain connectivity surely holds).</p>
<p>However, we can also use the fact that our graph is complete to make the shuffling algorithm significantly faster (by not having to look for existing nodes first). The fact that we deal on pure numpy arrays also allows faster shuffling than with the high level graph objects used in networkx.</p>
<p>First we define our own random/lattice shuffling functions:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[47]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">lattice_reference</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">niter</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">D</span><span class="o">=</span><span class="kc">None</span><span class="p">,</span> <span class="n">seed</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">2</span><span class="o">**</span><span class="mi">30</span><span class="p">))):</span>
    <span class="sd">&quot;&quot;&quot;Latticize the given graph by swapping edges. Works similar to networkx&#39; lattice reference.&quot;&quot;&quot;</span>
    <span class="kn">from</span> <span class="nn">networkx.utils</span> <span class="kn">import</span> <span class="n">cumulative_distribution</span><span class="p">,</span> <span class="n">discrete_sequence</span>

    <span class="c1"># Instead of choosing uniformly at random from a generated edge list,</span>
    <span class="c1"># this algorithm chooses nonuniformly from the set of nodes with</span>
    <span class="c1"># probability weighted by degree.</span>
    <span class="n">G</span> <span class="o">=</span> <span class="n">G</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
    <span class="n">keys</span> <span class="o">=</span> <span class="p">[</span><span class="n">i</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">G</span><span class="p">))]</span>
    <span class="n">degrees</span> <span class="o">=</span> <span class="n">weighted_node_degree</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>
    <span class="n">cdf</span> <span class="o">=</span> <span class="n">cumulative_distribution</span><span class="p">(</span><span class="n">degrees</span><span class="p">)</span>  <span class="c1"># cdf of degree</span>

    <span class="n">nnodes</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>
    <span class="n">nedges</span> <span class="o">=</span> <span class="n">nnodes</span> <span class="o">*</span><span class="p">(</span><span class="n">nnodes</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span> <span class="o">//</span> <span class="mi">2</span> <span class="c1"># NOTE: assuming full connectivity</span>
    <span class="k">if</span> <span class="n">D</span> <span class="ow">is</span> <span class="kc">None</span><span class="p">:</span>
        <span class="n">D</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">((</span><span class="n">nnodes</span><span class="p">,</span> <span class="n">nnodes</span><span class="p">))</span>
        <span class="n">un</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">nnodes</span><span class="p">)</span>
        <span class="n">um</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="n">nnodes</span> <span class="o">-</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span>
        <span class="n">u</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">append</span><span class="p">((</span><span class="mi">0</span><span class="p">,),</span> <span class="n">np</span><span class="o">.</span><span class="n">where</span><span class="p">(</span><span class="n">un</span> <span class="o">&lt;</span> <span class="n">um</span><span class="p">,</span> <span class="n">un</span><span class="p">,</span> <span class="n">um</span><span class="p">))</span>

        <span class="k">for</span> <span class="n">v</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">int</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">ceil</span><span class="p">(</span><span class="n">nnodes</span> <span class="o">/</span> <span class="mi">2</span><span class="p">))):</span>
            <span class="n">D</span><span class="p">[</span><span class="n">nnodes</span> <span class="o">-</span> <span class="n">v</span> <span class="o">-</span> <span class="mi">1</span><span class="p">,</span> <span class="p">:]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">u</span><span class="p">[</span><span class="n">v</span> <span class="o">+</span> <span class="mi">1</span> <span class="p">:],</span> <span class="n">u</span><span class="p">[:</span> <span class="n">v</span> <span class="o">+</span> <span class="mi">1</span><span class="p">])</span>
            <span class="n">D</span><span class="p">[</span><span class="n">v</span><span class="p">,</span> <span class="p">:]</span> <span class="o">=</span> <span class="n">D</span><span class="p">[</span><span class="n">nnodes</span> <span class="o">-</span> <span class="n">v</span> <span class="o">-</span> <span class="mi">1</span><span class="p">,</span> <span class="p">:][::</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>

    <span class="n">niter</span> <span class="o">=</span> <span class="n">niter</span> <span class="o">*</span> <span class="n">nedges</span>
    <span class="n">ntries</span> <span class="o">=</span> <span class="nb">int</span><span class="p">(</span><span class="n">nnodes</span> <span class="o">*</span> <span class="n">nedges</span> <span class="o">/</span> <span class="p">(</span><span class="n">nnodes</span> <span class="o">*</span> <span class="p">(</span><span class="n">nnodes</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span> <span class="o">/</span> <span class="mi">2</span><span class="p">))</span>
    <span class="n">swapcount</span> <span class="o">=</span> <span class="mi">0</span>

    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">niter</span><span class="p">):</span>
        <span class="n">n</span> <span class="o">=</span> <span class="mi">0</span>
        <span class="k">while</span> <span class="n">n</span> <span class="o">&lt;</span> <span class="n">ntries</span><span class="p">:</span>
            <span class="c1"># pick two random edges without creating edge list</span>
            <span class="c1"># choose source node indices from discrete distribution</span>
            <span class="p">(</span><span class="n">ai</span><span class="p">,</span> <span class="n">bi</span><span class="p">,</span> <span class="n">ci</span><span class="p">,</span> <span class="n">di</span><span class="p">)</span> <span class="o">=</span> <span class="n">discrete_sequence</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="n">cdistribution</span><span class="o">=</span><span class="n">cdf</span><span class="p">,</span> <span class="n">seed</span><span class="o">=</span><span class="n">seed</span><span class="p">)</span>
            <span class="k">if</span> <span class="nb">len</span><span class="p">(</span><span class="nb">set</span><span class="p">((</span><span class="n">ai</span><span class="p">,</span> <span class="n">bi</span><span class="p">,</span> <span class="n">ci</span><span class="p">,</span> <span class="n">di</span><span class="p">)))</span> <span class="o">&lt;</span> <span class="mi">4</span><span class="p">:</span>
                <span class="k">continue</span>  <span class="c1"># picked same node twice</span>
            <span class="n">a</span> <span class="o">=</span> <span class="n">keys</span><span class="p">[</span><span class="n">ai</span><span class="p">]</span>  <span class="c1"># convert index to label</span>
            <span class="n">b</span> <span class="o">=</span> <span class="n">keys</span><span class="p">[</span><span class="n">bi</span><span class="p">]</span>
            <span class="n">c</span> <span class="o">=</span> <span class="n">keys</span><span class="p">[</span><span class="n">ci</span><span class="p">]</span>
            <span class="n">d</span> <span class="o">=</span> <span class="n">keys</span><span class="p">[</span><span class="n">di</span><span class="p">]</span>

            <span class="n">is_closer</span> <span class="o">=</span> <span class="n">D</span><span class="p">[</span><span class="n">ai</span><span class="p">,</span> <span class="n">bi</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="n">D</span><span class="p">[</span><span class="n">ci</span><span class="p">,</span> <span class="n">di</span><span class="p">]</span>
            <span class="n">is_larger</span> <span class="o">=</span> <span class="p">(</span><span class="n">G</span><span class="p">[</span><span class="n">ai</span><span class="p">,</span> <span class="n">bi</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="n">G</span><span class="p">[</span><span class="n">ci</span><span class="p">,</span> <span class="n">di</span><span class="p">])</span>
            <span class="k">if</span> <span class="n">is_closer</span> <span class="ow">and</span> <span class="n">is_larger</span><span class="p">:</span>
                <span class="c1"># only swap if we get closer to the diagonal</span>

                <span class="n">ab</span> <span class="o">=</span> <span class="n">G</span><span class="p">[</span><span class="n">a</span><span class="p">,</span> <span class="n">b</span><span class="p">]</span>
                <span class="n">cd</span> <span class="o">=</span> <span class="n">G</span><span class="p">[</span><span class="n">c</span><span class="p">,</span> <span class="n">d</span><span class="p">]</span>
                <span class="n">G</span><span class="p">[</span><span class="n">a</span><span class="p">,</span> <span class="n">b</span><span class="p">]</span> <span class="o">=</span> <span class="n">cd</span>
                <span class="n">G</span><span class="p">[</span><span class="n">b</span><span class="p">,</span> <span class="n">a</span><span class="p">]</span> <span class="o">=</span> <span class="n">cd</span>
                <span class="n">G</span><span class="p">[</span><span class="n">c</span><span class="p">,</span> <span class="n">d</span><span class="p">]</span> <span class="o">=</span> <span class="n">ab</span>
                <span class="n">G</span><span class="p">[</span><span class="n">d</span><span class="p">,</span> <span class="n">c</span><span class="p">]</span> <span class="o">=</span> <span class="n">ab</span>

                <span class="n">swapcount</span> <span class="o">+=</span> <span class="mi">1</span>
                <span class="k">break</span>
            <span class="n">n</span> <span class="o">+=</span> <span class="mi">1</span>
    <span class="k">return</span> <span class="n">G</span>


<span class="k">def</span> <span class="nf">random_reference</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">niter</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">D</span><span class="o">=</span><span class="kc">None</span><span class="p">,</span> <span class="n">seed</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">2</span><span class="o">**</span><span class="mi">30</span><span class="p">))):</span>
    <span class="sd">&quot;&quot;&quot;Latticize the given graph by swapping edges. Works similar to networkx&#39; random reference.&quot;&quot;&quot;</span>
    <span class="kn">from</span> <span class="nn">networkx.utils</span> <span class="kn">import</span> <span class="n">cumulative_distribution</span><span class="p">,</span> <span class="n">discrete_sequence</span>

    <span class="c1"># Instead of choosing uniformly at random from a generated edge list,</span>
    <span class="c1"># this algorithm chooses nonuniformly from the set of nodes with</span>
    <span class="c1"># probability weighted by degree.</span>
    <span class="n">G</span> <span class="o">=</span> <span class="n">G</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
    <span class="n">keys</span> <span class="o">=</span> <span class="p">[</span><span class="n">i</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">G</span><span class="p">))]</span>
    <span class="n">degrees</span> <span class="o">=</span> <span class="n">weighted_node_degree</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>
    <span class="n">cdf</span> <span class="o">=</span> <span class="n">cumulative_distribution</span><span class="p">(</span><span class="n">degrees</span><span class="p">)</span>  <span class="c1"># cdf of degree</span>

    <span class="n">nnodes</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>
    <span class="n">nedges</span> <span class="o">=</span> <span class="n">nnodes</span> <span class="o">*</span><span class="p">(</span><span class="n">nnodes</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span> <span class="o">//</span> <span class="mi">2</span> <span class="c1"># NOTE: assuming full connectivity</span>
    <span class="k">if</span> <span class="n">D</span> <span class="ow">is</span> <span class="kc">None</span><span class="p">:</span>
        <span class="n">D</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">((</span><span class="n">nnodes</span><span class="p">,</span> <span class="n">nnodes</span><span class="p">))</span>
        <span class="n">un</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">nnodes</span><span class="p">)</span>
        <span class="n">um</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="n">nnodes</span> <span class="o">-</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span>
        <span class="n">u</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">append</span><span class="p">((</span><span class="mi">0</span><span class="p">,),</span> <span class="n">np</span><span class="o">.</span><span class="n">where</span><span class="p">(</span><span class="n">un</span> <span class="o">&lt;</span> <span class="n">um</span><span class="p">,</span> <span class="n">un</span><span class="p">,</span> <span class="n">um</span><span class="p">))</span>

        <span class="k">for</span> <span class="n">v</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">int</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">ceil</span><span class="p">(</span><span class="n">nnodes</span> <span class="o">/</span> <span class="mi">2</span><span class="p">))):</span>
            <span class="n">D</span><span class="p">[</span><span class="n">nnodes</span> <span class="o">-</span> <span class="n">v</span> <span class="o">-</span> <span class="mi">1</span><span class="p">,</span> <span class="p">:]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">u</span><span class="p">[</span><span class="n">v</span> <span class="o">+</span> <span class="mi">1</span> <span class="p">:],</span> <span class="n">u</span><span class="p">[:</span> <span class="n">v</span> <span class="o">+</span> <span class="mi">1</span><span class="p">])</span>
            <span class="n">D</span><span class="p">[</span><span class="n">v</span><span class="p">,</span> <span class="p">:]</span> <span class="o">=</span> <span class="n">D</span><span class="p">[</span><span class="n">nnodes</span> <span class="o">-</span> <span class="n">v</span> <span class="o">-</span> <span class="mi">1</span><span class="p">,</span> <span class="p">:][::</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>

    <span class="n">niter</span> <span class="o">=</span> <span class="n">niter</span> <span class="o">*</span> <span class="n">nedges</span>
    <span class="n">ntries</span> <span class="o">=</span> <span class="nb">int</span><span class="p">(</span><span class="n">nnodes</span> <span class="o">*</span> <span class="n">nedges</span> <span class="o">/</span> <span class="p">(</span><span class="n">nnodes</span> <span class="o">*</span> <span class="p">(</span><span class="n">nnodes</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span> <span class="o">/</span> <span class="mi">2</span><span class="p">))</span>
    <span class="n">swapcount</span> <span class="o">=</span> <span class="mi">0</span>

    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">niter</span><span class="p">):</span>
        <span class="n">n</span> <span class="o">=</span> <span class="mi">0</span>
        <span class="k">while</span> <span class="n">n</span> <span class="o">&lt;</span> <span class="n">ntries</span><span class="p">:</span>
            <span class="c1"># pick two random edges without creating edge list</span>
            <span class="c1"># choose source node indices from discrete distribution</span>
            <span class="p">(</span><span class="n">ai</span><span class="p">,</span> <span class="n">bi</span><span class="p">,</span> <span class="n">ci</span><span class="p">,</span> <span class="n">di</span><span class="p">)</span> <span class="o">=</span> <span class="n">discrete_sequence</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="n">cdistribution</span><span class="o">=</span><span class="n">cdf</span><span class="p">,</span> <span class="n">seed</span><span class="o">=</span><span class="n">seed</span><span class="p">)</span>
            <span class="k">if</span> <span class="nb">len</span><span class="p">(</span><span class="nb">set</span><span class="p">((</span><span class="n">ai</span><span class="p">,</span> <span class="n">bi</span><span class="p">,</span> <span class="n">ci</span><span class="p">,</span> <span class="n">di</span><span class="p">)))</span> <span class="o">&lt;</span> <span class="mi">4</span><span class="p">:</span>
                <span class="k">continue</span>  <span class="c1"># picked same node twice</span>
            <span class="n">a</span> <span class="o">=</span> <span class="n">keys</span><span class="p">[</span><span class="n">ai</span><span class="p">]</span>  <span class="c1"># convert index to label</span>
            <span class="n">b</span> <span class="o">=</span> <span class="n">keys</span><span class="p">[</span><span class="n">bi</span><span class="p">]</span>
            <span class="n">c</span> <span class="o">=</span> <span class="n">keys</span><span class="p">[</span><span class="n">ci</span><span class="p">]</span>
            <span class="n">d</span> <span class="o">=</span> <span class="n">keys</span><span class="p">[</span><span class="n">di</span><span class="p">]</span>


            <span class="c1"># only swap if we get closer to the diagonal</span>

            <span class="n">ab</span> <span class="o">=</span> <span class="n">G</span><span class="p">[</span><span class="n">a</span><span class="p">,</span> <span class="n">b</span><span class="p">]</span>
            <span class="n">cd</span> <span class="o">=</span> <span class="n">G</span><span class="p">[</span><span class="n">c</span><span class="p">,</span> <span class="n">d</span><span class="p">]</span>
            <span class="n">G</span><span class="p">[</span><span class="n">a</span><span class="p">,</span> <span class="n">b</span><span class="p">]</span> <span class="o">=</span> <span class="n">cd</span>
            <span class="n">G</span><span class="p">[</span><span class="n">b</span><span class="p">,</span> <span class="n">a</span><span class="p">]</span> <span class="o">=</span> <span class="n">cd</span>
            <span class="n">G</span><span class="p">[</span><span class="n">c</span><span class="p">,</span> <span class="n">d</span><span class="p">]</span> <span class="o">=</span> <span class="n">ab</span>
            <span class="n">G</span><span class="p">[</span><span class="n">d</span><span class="p">,</span> <span class="n">c</span><span class="p">]</span> <span class="o">=</span> <span class="n">ab</span>

            <span class="n">swapcount</span> <span class="o">+=</span> <span class="mi">1</span>
            <span class="k">break</span>

    <span class="k">return</span> <span class="n">G</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>To visualize what our defined random and lattice shuffling does compared to networkx, we plot them next to a (binarized) version of the same graph, shuffled with networkx.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[48]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">networkx</span> <span class="k">as</span> <span class="nn">nx</span>

<span class="k">def</span> <span class="nf">random_reference_nx</span><span class="p">(</span><span class="n">matrix</span><span class="p">,</span> <span class="n">niter</span><span class="o">=</span><span class="mi">5</span><span class="p">):</span>
  <span class="n">G</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">convert_matrix</span><span class="o">.</span><span class="n">from_numpy_array</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
  <span class="n">G_ref</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">algorithms</span><span class="o">.</span><span class="n">smallworld</span><span class="o">.</span><span class="n">random_reference</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">niter</span><span class="o">=</span><span class="n">niter</span><span class="p">)</span>
  <span class="k">return</span> <span class="n">nx</span><span class="o">.</span><span class="n">convert_matrix</span><span class="o">.</span><span class="n">to_numpy_array</span><span class="p">(</span><span class="n">G_ref</span><span class="p">)</span>

<span class="k">def</span> <span class="nf">lattice_referefnce_nx</span><span class="p">(</span><span class="n">matrix</span><span class="p">,</span> <span class="n">niter</span><span class="o">=</span><span class="mi">5</span><span class="p">):</span>
  <span class="n">G</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">convert_matrix</span><span class="o">.</span><span class="n">from_numpy_array</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
  <span class="n">G_ref</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">algorithms</span><span class="o">.</span><span class="n">smallworld</span><span class="o">.</span><span class="n">lattice_reference</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">niter</span><span class="o">=</span><span class="n">niter</span><span class="p">)</span>
  <span class="k">return</span> <span class="n">nx</span><span class="o">.</span><span class="n">convert_matrix</span><span class="o">.</span><span class="n">to_numpy_array</span><span class="p">(</span><span class="n">G_ref</span><span class="p">)</span>

<span class="c1"># create a graph with a sin like structure</span>
<span class="n">g</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">vstack</span><span class="p">([</span><span class="n">np</span><span class="o">.</span><span class="n">sin</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="n">i</span><span class="p">,</span><span class="mi">7</span><span class="o">+</span><span class="n">i</span><span class="p">,</span> <span class="mi">25</span><span class="p">))</span><span class="o">*</span><span class="mf">0.3</span><span class="o">+</span><span class="mf">0.5</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">25</span><span class="p">)])</span>
<span class="c1"># mirror it</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">g</span><span class="p">)):</span>
  <span class="k">for</span> <span class="n">ii</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">g</span><span class="p">)):</span>
    <span class="n">g</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">ii</span><span class="p">]</span> <span class="o">=</span> <span class="n">g</span><span class="p">[</span><span class="n">ii</span><span class="p">,</span><span class="n">i</span><span class="p">]</span>
<span class="n">g</span> <span class="o">=</span> <span class="n">remove_self_connections</span><span class="p">(</span><span class="n">g</span><span class="p">)</span>


<span class="c1"># plot actual, random and lattice shuffled graphs side by side</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n\n</span><span class="s2">Using our own shuffling functions: </span><span class="se">\n\n</span><span class="s2">&quot;</span><span class="p">)</span>
<span class="n">plot_graph</span><span class="p">(</span><span class="n">g</span><span class="p">,</span> <span class="n">title</span><span class="o">=</span><span class="s2">&quot;Original weighted Graph&quot;</span><span class="p">)</span>
<span class="n">plot_graph</span><span class="p">(</span><span class="n">random_reference</span><span class="p">(</span><span class="n">g</span><span class="p">,</span> <span class="n">niter</span><span class="o">=</span><span class="mi">5</span><span class="p">),</span> <span class="n">title</span><span class="o">=</span><span class="s2">&quot;Weighted Graph shuffled with our own random ref&quot;</span><span class="p">)</span>
<span class="n">plot_graph</span><span class="p">(</span><span class="n">lattice_reference</span><span class="p">(</span><span class="n">g</span><span class="p">,</span> <span class="n">niter</span><span class="o">=</span><span class="mi">5</span><span class="p">),</span> <span class="n">title</span><span class="o">=</span><span class="s2">&quot;Weighted Graph shuffled with our own lattice ref&quot;</span><span class="p">)</span>


<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n\n</span><span class="s2">Using networkx on a binarized graph: </span><span class="se">\n\n</span><span class="s2">&quot;</span><span class="p">)</span>
<span class="n">plot_graph</span><span class="p">(</span><span class="n">g_bin</span><span class="p">,</span> <span class="n">title</span><span class="o">=</span><span class="s2">&quot;Original Graph (binarized)&quot;</span><span class="p">)</span>
<span class="n">g_bin</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="n">g</span><span class="p">)</span>
<span class="n">plot_graph</span><span class="p">(</span><span class="n">random_reference_nx</span><span class="p">(</span><span class="n">g_bin</span><span class="p">,</span> <span class="n">niter</span><span class="o">=</span><span class="mi">5</span><span class="p">),</span> <span class="n">title</span><span class="o">=</span><span class="s2">&quot;Binary graph shuffled with networkx random ref&quot;</span><span class="p">)</span>
<span class="n">plot_graph</span><span class="p">(</span><span class="n">lattice_reference_nx</span><span class="p">(</span><span class="n">g_bin</span><span class="p">,</span> <span class="n">niter</span><span class="o">=</span><span class="mi">5</span><span class="p">),</span> <span class="n">title</span><span class="o">=</span><span class="s2">&quot;Binary graph shuffled with networkx lattice ref&quot;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>

Using our own shuffling functions: 


</pre>
</div>
</div>

<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAW4AAAEWCAYAAABG030jAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADh0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uMy4yLjIsIGh0dHA6Ly9tYXRwbG90bGliLm9yZy+WH4yJAAAgAElEQVR4nO3deZxcVZn/8c+XbJ2tydIBEggEBHUQJQIigjooLoiDoOOg6Ci4TPzNzw1/Ou6jqOO4jDqLzujEZRQXXEBHcBgQwXVUVoMQUUEgJCF7ZyVrdz+/P+7todJ2dz2VdHXVbb7v16te6br11Lnn1q2cvn3uec5RRGBmZtVxQKsrYGZmjXHDbWZWMW64zcwqxg23mVnFuOE2M6sYN9xmZhXjhnuMkfROSZ8b6dhEWSHp6JEoa4jyGzmuiyV9pYl1aWr5+0LSfZKe0ep62Ohww93GJF0o6XZJ2yWtlvRpSTOGe09E/H1EvDpTfiOxrTaSdW12IydpuqRPlPt5UNL9ki6T9MRm7dMeXtxwtylJbwY+AvwNcCBwCnAEcK2kiUO8Z/zo1dAGI2kScD3wWODPgE7gT4CvA88Z4j0+b9YQN9xtSFIn8D7g9RFxdUTsiYj7gPOABcBflnEXl1dyX5G0Bbhw4J/xkl4uaZmkDZL+tvZqszZW0oKyu+OC8gpxvaR31ZRzsqRfSNokaZWkTw31C2TAsTxN0u01z6+VdFPN859KOrf8eZ6kyyWtk3SvpDfUxKWPqzRR0iWStkpaKumk8n1fBg4HrpS0TdJby+2nSPp5eXy3STq9Zl9HSvpxWda1QNcwh/wy4DDg3Ii4IyJ6I+LBiLgsIi6uKTMkvVbSXcBd5bZ/lrRc0hZJt0h6yoDjv0zSN8p63Crp+AH7Xijp15I2l3Edw9TTKswNd3s6FegAvl27MSK2AVcBz6zZfA5wGTAD+GptvKRjgX8DXgrMpbhyP7TOvp8MPAo4A3iPpD8pt/cCb6JotJ5Uvv5/E8fyS+AYSV2SJgCPA+aV3QmTgZOAn0o6ALgSuK2s4xnARZKePbDA5HE9j+IqdwZwBfApgIh4GXA/cHZETIuIj0o6FPgv4O+AWcBbgMslzSnL+hpwS3nsHwAuGOZ4nwFcExEPJj6bc4EnAseWz28CFpZ1+BrwrQGN7znAt2pe/8/yM+13HnAmcCTF53xhog5WQW6421MXsD4iegZ5bRV7X/H9IiL+MyL6ImLHgNgXAldGxM8iYjfwHqDe5DTvi4gdEXEbRSN6PEBE3BIRv4yInvLq/9+BP613IGWdbgKeCpxYlvk/wGkU3T93RcQG4AnAnIh4f0Tsjoh7gM8CLx6k2Mxx/SwiroqIXuDL/ccxhL8Erirj+yLiWuBm4CxJh5d1+9uI2BURP6H4BTOULmB1/xNJC8ur+C2Sfjcg9kMR0d1/3iLiKxGxofyMPw5Movgl2u+W8sp9D/AJil/up9S8/i8R8UBEdJd1XDhMPa3C3LfWntYDXZLGD9J4zy1f77d8mHLm1b4eEdslbaiz79U1P28HpgFIeiRFY3ESMIXiu3NLnbL6/Rg4HVhR/ryRotHfVT6Hov9+nqRNNe8bB/x0kPIyxzXwODqG+Dz79/0Xks6u2TYB+GG5r40DrqCXAfMHKQdgA8U56q/bEmBG2Y0zcFTMXudO0luAV5X7DIr+8a7B4iOiT9KKMrbfwGOufc3GEF9xt6dfUDRqL6jdKGkaxQ2u62o2D3cFvYqiv7X//ZOB2ftYp08DvwWOiYhO4J2Aku/tb7ifWv78Y4qG+095qOFeDtwbETNqHtMj4qxBytvf4xr4mS0Hvjxg31Mj4sPlvmZKmloTf/gwZV8HPGtAfN16lP3Zb6Xo7pgZETOAzez9Gc+viT+A4jN4ILEfG2PccLehiNhMcXPyk5LOlDRB0gLgmxRXrV9OFnUZcLakU8sbiReTb2wHmg5sAbZJejTw1w289+cUf/KfDNwYEUsprnKfCPykjLkR2CrpbZImSxon6ThJTxikvP09rjXAUTXPv1KW9+xyvx2STpd0WEQso+g2eZ+kiZKeDJw9WKGlSyga+++U9R9X9lOfVKdO04EeYB0wXtJ7KK64a50o6QUqRqFcRPHL/ZfJY7YxxA13m4qIj1Jc1X6MosG8geLK8IyI2JUsYynweoqbdKuAbcBaiv/wjXoL8BJgK0Xf8zeybyy7GW4FlpZ90lD8VbEsItaWMb0Uw+cWAvdSdAd9juLG40gf14eAd5d9z2+JiOUUN/7eSdFwLqcYhtn//+MlFL9kuoH3UjTOQx3rTuBpwG8obnhuAX5H0U9+3jB1uga4Gvg9RVfMTv64G+y7wIsouppeBryg7O+2hxl5IYWHj7KrZRNFd8e9ra7PSBmrx1VL0sXA0RHxl62ui7Wer7jHOElnS5pS9rl+DLgduK+1tdp/Y/W4zDKa1nBLmi/ph5J+UyZAvLHcfrGklZKWlI/Bbj7ZyDmH4gbWA8AxwItjbPyZNVaPy8YYSV+QtFbSHUO8Lkn/IunuMoHqhLplNuu7LmkuMDcibpU0nWLo2LkU/XzbIuJjTdmxmVkbkfRUivswl0TEcYO8fhbFPZuzKO6l/HNEDDuvTdOuuCNiVUTcWv68FbiT+ll7ZmZjSpm01T1MyDkUjXpExC8pxv3PHSZ+dBJwyqFsj6cYGXEa8DpJL6cYZvXmiNg4yHsWAYsADhg38cQp0+YMDPkjMS4/IqxvXDqUvuSnFI18muP70qETkrETxw2WWzJEmepNxx6gkf+rrCfyJ2B3Aydrd08utq8nf82invz3SvlTwAHJ2AZOFerLn6vsaY0GBlrGAfngBr4CjNuQmUGgsJWN6yOifoMxjGc/bWps6K7/wd/y611LKUYA9VscEYsb3N2h7D2CaEW5bdVQb2h6w13e8b8cuCgitkj6NMV8D1H++3HglQPfVx78YoDpMw6LE57yxrr72j09/59x58x87I7hphSqsasr3xgfMCc/Iu+gWVtScYdP31Q/qHRIx+Z07LRx+br2Jv+I696dyU8pLN8+7Ey2e1mxKRe7dUN+/+PXTagfVOpYlw6lozvXcnZsyn+vxj/YwC/k3tz++xq4IOqZkm+Nd83I/x+c8cVfpGN/EJctSwcPYUN3LzdeM1yeVWHc3Lt2RkS9MfojrqkNdzkBzuXAVyPi2wARsabm9c8C32tmHczMGhVAH/lfmPtpJXtPoXBYuW1IzRxVIuDzwJ0R8Yma7bV9N88HBr3TambWKkGwJ3rrPkbIFcDLy9ElpwCbI2LIbhJo7hX3aRTZXbdLWlJueydwvqSFFL/U7gNe08Q6mJntk5G64pZ0KcVcPV3lxGDvpZjEjIj4DMVUzWcBd1NMDvaKemU2reGOiJ8x+PwRVzVrn2ZmIyEIekdoqHREnF/n9QBe20iZntbVzGwQfXWnrm8dN9xmZgME0OuG28ysWnzFbWZWIQHsaeOpbyrRcIdE74T6SQAdG/Jpa5PX5U/KgX/IJSD0TM0nH+ycmV+Ae+usyam4W+YclC6zZ05+GufO2fmstfkH5pKADp2STwA6fsawQ1r3csKM4VZye8i2+ZPSZa7e+UdTgg9p2ZaZ6di13dNTcbE+X9eOdRPzsfUWseuP25gfXTFxaz62kaSaTRc+KR3Lf1yWjx1CEO4qMTOrlIBkYmlLuOE2MxugyJxsX264zcz+iOjd5+VZm88Nt5nZAMXNSTfcZmaVUYzjdsNtZlYpfb7iNjOrDl9xj4A90+GBP60/A23Huvw46uwYVoCO7tz95Qnb8tM8di7Ljzmffn/uC9TbkZ+ld3dnfnGAHbPyY5Pv7srFLu3Kf1YT5uysH1SaOys3Pnz+tPyiE/Mm52OPnro2HbvnkNz3dd3uaekyVzzYwKITG3Ox3RumpMt85KIb07G7n3tyOnZSA4tJjIRA6UVBWqESDbeZ2WhzV4mZWYUEYncji2KOMjfcZmYDFAk47ioxM6sU35w0M6uQCNEbvuI2M6uUPl9xm5lVR3Fzsn2bx/atmZlZi/jm5AiYPnUHT3nS0rpx92/LJx88sCk/OX73ulwCwsR1+aSWxhKAchMDT9qcT2qZvC6/kMKUNfmJifvG577se6Y1sujE1HTshtm52JVz5qbL7O3anY6d1bUtHTu/M7voRD4B6MRZuYUkAE6etSwVd+Of58/V7xfnk2rmXZ9vGCd15xPWRkqvx3GbmVWHMyfNzCqoz6NKzMyqo5hkyg23mVllBGKPU97NzKojAifgmJlVi5yAY2ZWJYGvuM3MKsc3J/fTAQo6x9dfBeXUrnvTZfZ25U/KpiMmp+JW7cgn9Szfkk8WWrs+twLKuPUT02V2rMuf+oaShTaO/GpBkzblk4U6l+X+vO2ZnD//uw7Mf647Z81Ox945Oxd725wGPqs529Oxh7/w9lTcyUvy+1/xh/z+d87sTMdOXpdPAhsJgbyQgplZlQSwx3OVmJlViTwft5lZlQTOnDQzq5x2vuJu2q8USfMl/VDSbyQtlfTGcvssSddKuqv8d2az6mBmti8iRF8cUPfRKs3ccw/w5og4FjgFeK2kY4G3A9dFxDHAdeVzM7O2UdycHFf30SpN6yqJiFXAqvLnrZLuBA4FzgFOL8O+BPwIeFuz6mFm1jivOYmkBcDjgRuAg8tGHWA1cPAQ71kELAIYN2sGV9y6sO5+pszOjyE9bGZ+cvrDpuZiHzV9TbrM4zofSMdun5cbR7x21/R0mcu25nuo1mzMj7fdsK4jFTdpfQOLTqxPhzI5uejExC35sclTV+XHkU97ID/euHfiyC86MfVbubHZAPdf9thU3In8Ol1mI/+vVszOf6/6xo1uf3Nxc7J9+7ib3nBLmgZcDlwUEVukhz6MiAhJg37TI2IxsBhg0oLDRnf0vZk97D1sMyclTaBotL8aEd8uN6+RNDciVkmaC6xtZh3MzBrV7pmTzRxVIuDzwJ0R8Ymal64ALih/vgD4brPqYGa2r/o4oO6jVZp5xX0a8DLgdklLym3vBD4MfFPSq4BlwHlNrIOZWcMiYE/fw7CrJCJ+BkOOYD+jWfs1M9tfRVfJw7DhNjOrsnbOnHTDbWY2wMN+OKCZWfW4q2S/Tdgq5l1f/0NsZGL2Rgb/3z3nsFScunalyzxo1tZ07BGdG1Nxh3RsTpe54KD86gi9B+W/wN1HTk3FrdzewKITm/OLTqzekNv/+LUNLDrRQAJQx4Z8ykHHptyiE1O/9ct0mQ/+xSnp2F3JxQm2LMglVUE+WQ3y/68AeqaOfnq515w0M6uQYlRJ6+YiqccNt5nZAO2egOOG28xsEO4qMTOrEI8qMTOrII8qMTOrkAjR44bbzKxa3FViZlYh7uMeAeoJJnX31I2bnEwogMZW1MgO/t85I5+osG3W5HTsLXMOSsX1zMmv1DJ99oPp2MNm5JMq5k/JxT52Rn4FoIUzVqRjtx02KRW3emc+Aej+rfkEoLXd+cSuo17yq1Tcjuc/MV3mhG35lX0mrsutQrRye/74G1kFqpGEtUb+b40UN9xmZhXicdxmZhXkcdxmZhUSAT0Px4UUzMyqzF0lZmYV4j5uM7MKCjfcZmbV4puT+6lnilh7Uv2J7zvyawMwKTmJPcDELbmxsZ331x9r3m/68vyXorcjd5Nkd2f+dO6YlR+be+/sfOydc3Kf1fiunekyD5m1JR17xPTcohPzJufHph89dW069sYz83M43/O1x6fiZl6bv0nWyHcw+/9l+Zb8+T+uMz8+v5HFRBrJexgJEWOgj1vSI4AVEbFL0unA44BLIiL/7TczqwzR28ajSrI1uxzolXQ0sBiYD3ytabUyM2uxCNV9tEr2b+u+iOiR9HzgkxHxSUm5fF0zs4oZK3OV7JF0PnABcHa5LTfRgZlZ1UTRz92usl0lrwCeBHwwIu6VdCTw5eZVy8ystfpQ3UerpK64I+I3kt4GHF4+vxf4SDMrZmbWKjEWbk5KOhtYAlxdPl8o6YpmVszMrJUi6j9aJfsr5WLgZGATQEQsAY5qUp3MzFpuLIwq2RMRm6W9KprPYNlP4zv3cPDT60+mv2pTfnL87vX5Af3ZCec71qeLpKM7/+t60uZcUsvkdfmFFKasaWDRifH5Pxn3TEsuOjFzarrMjbPysavmHJKK621g0YljLrw5HXvykvxCBttW5xKLts7Of1cbSezKfgfXrp+WLnP7vPqJcv2O6MwlS0F+MZGRUlxRV39UyVJJLwHGSToGeAPw8+ZVy8ystdp5OGD2Uur1wGOAXcClwBbgomZVysys1dq5jzs7qmQ78K7yYWY2pgWir41HlQzbcEu6kiKJaFAR8bwRr5GZWRto4/ybul0lHwM+DtwL7AA+Wz62AX8Y7o2SviBpraQ7arZdLGmlpCXl46z9q76ZWRNEhUeVRMSPASR9PCJOqnnpSkn1brV/EfgUcMmA7f8YER9rtKJmZqOqjS+5s504UyX977jtMuV92DFaEfEToHs/6mZm1jKVveKu8SbgR5LuAQQcASzax32+TtLLgZuBN0fEoIM5JS3q38ekg6bv467MzBoXQF9f+w4HzI4qubocv/3octNvI2LXPuzv08AHKD6XD1D0n79yiH0uppj7m7mPmRmndt1bt/Dervxd4C0LOtKxK7fnVgBpZKWQRpIaxq3PJTV0rMuvgDOpgb+FOjbmc60mbMsloBy4KZ8A07ks/x+oZ3LuO9BxRT6p5q4vnlQ/qHRcX36248On59YhuaXr4HSZ2dWSIJ/Ylf3+Aazdlb/IOqRjczq2p4GEqRERQBuP486ugDMBeA3w1HLTjyT9e0Q09GlGxJqaMj8LfK+R95uZjZaxMK3rp4ETgX8rHyeW2xoiaW7N0+cDdwwVa2bWUpF4tEj2b+snRMTxNc+vl3TbcG+QdClwOtAlaQXwXuB0SQspDvk+iqt4M7M209qbj/VkG+5eSY+IiD8AlCNMhu0gi4jzB9n8+QbrZ2bWGm3cVZJtuP8G+OGAUSWvaFqtzMxaKSDGwKiS68pRJY8qN/1uH0eVmJlVREUbbklPHeKlJ0rqT7IxMxt7KtxV8jeDbAvgccB8IDdrvplZ1VS14Y6Is2ufSzoNeDewmmKO7lGxaddkvv2H4+vGzZuRH9B/+LT86huPmr6mfhBwXOcD6TIbWSkkm9SwfFs+AWj1xs50bPe6/Aosk9a3drWgzq/+IhW383knp8scty5/fdKMBJSeg3any9zdmfv8Ib9iUiOJXY18BxfM2ZCOnT77wXTsiBgjCThnAH9LcTh/HxHXNrVWZmYt1s4JOPX6uJ9LsXjCZuDdEfGzUamVmVmrVXhUyZXACmAD8FZJb6190QspmNlYpapecQNPG5VamJm1kxantNdTr+F+KfDfwA8iYuso1MfMrA2orW9O1ptk6vPA8cBVkq6T9DZJ9Yd3mJlVXVUnmYqIG4AbgIslzQaeBbxZ0uOAW4GrI+Kbza+mmdkoy09DP+rSAzQjYgNwaflA0onAmU2q1160ZRwd19Yfd/xAV35s8j1zDs3vvyuX3X/QrHxv0vzkJPoA8ybnYhsZF9s7Jz/hfveCYVep28vK7Qem4pZvzo/37TznznTslpc+KRU3ZW1+KvlGxjEv2zozHbvgoNz56mxgDPOOWfn9T1mTu2TsyH+tWNWdO//Q2HfwsBn5/y8jMld0m4/jTn1ykt4oqVOFz0m6FeiKiA82uX5mZi2hqP9IlSOdKel3ku6W9PZBXr9Q0jpJS8rHq+uVmf2V98qI2ELRVTIbeBnwoeR7zcyqZwT6uCWNA/4VeA5wLHC+pGMHCf1GRCwsH5+rV2624e7/m+Es4JKIWEo7T51lZtYeTgbujoh7ImI38HXgnP0tNNtw3yLp+xQN9zWSptPWXfdmZvsn2VXSJenmmseiAcUcCiyveb6i3DbQn0v6taTLJM2vV7fsXZdXAQuBeyJieznCxAspmNnYFGRT3tdHxEn7ubcrgUsjYpek1wBfAp4+3BvqzVVywoBNR0nuITGzh4GRGae9kmIK7H6Hldse2k0xYq/f54CP1iu03hX3x4d5LajzW8HMrKpGaK6Sm4BjJB1J0WC/GHjJXvuR5kbEqvLp84C641/rJeB4rhIze3gagYY7InokvQ64hmLhmS9ExFJJ7wdujogrgDdIeh7QA3QDF9YrNzsf9xTg/wGHR8Si/vUnI+J7+3Y4jRm/M5h5V/0kmL578t04PVPzk+PvnNGRits2K7/gwK+6DkrH3nRQLlmkkcnmG0loOHRKfoGKxxy4qn4QsPv0XBzAmu/+STpWP8h9B6auzv+v7OhOh7K6O58E1ntQbmzA/APz5+rurnwCTt/43P47NubHIWxYl/u/AtB9ZD6xa/6U/GcwYkYopT0irgKuGrDtPTU/vwN4RyNlZkeV/AewGzi1fL4S+LtGdmRmVhWZESWtnPY123A/IiI+CuwBiIjteBy3mY1lfar/aJHscMDdkiZT/vEg6RFAbgIPM7MKqvJCCv3eC1wNzJf0VeA0Eh3oZmaVVfWGOyKuLSeWOoWii+SNEdHAOt1mZhXS4j7sevLzVUIHsLF8z7GSiIifNKdaZmYtVvWGW9JHgBcBS3lojpIA3HCb2ZikNp6NKXvFfS7FuG3fkDQza7Fsw30PMIEWjSTp6RAbj5lUN66RRIGJW3rTsZ3396Tipi/PDw/q7civ/rG7M3eads7Mrypzb1c+9s6u/Od6zOt/mYp7/K/SRbJ088gnoPROyH/+DSWgrG8gAWV3LgGlkQSopV357/WeabkktAnb8mVOWj8hHZtdLQngsTMeSMeOmKp3lQDbgSWSrqOm8Y6INzSlVmZmrTRGbk5eUT7MzB4eqt5wR8SXml0RM7O2UvWGW9JpwMXAEeV7BEREHNW8qpmZtYYYG6NKPg+8CbgFSN2pkPQF4M+AtRFxXLltFvANYAFwH3BeRGxsrMpmZk3W5n3c2VvrmyPivyNibURs6H/Uec8XgTMHbHs7cF1EHANcVz43M2s/I7DKe7NkG+4fSvoHSU+SdEL/Y7g3lFmVA2cyPodiPTXKf89trLpmZqOkjRvubFfJE8t/axfF3Jelyw6uWaJnNXDwUIHlasmLAMZ3HciOZ2ytW/jGDfmFDCauzY837aj3t0V/XHf+TE7anO9Am7wut5DClDX5/Wcn0QeYcM1N6di7PnlKKu6IPbeny2zGOObsGGaAiVvz45g71uW/V8u358bSHz9jZf2g0oQ5O9OxO2fmxpFP2pT7/gF0NDCD0fLN+VyChTNW5AseIe3cVZIdVTLiS5hFREhDfzQRsRhYDNBx9KFt/BGa2ZjUxq1OepIpSc8FHkMx2RQAEfH+Bve3pn9hTElzgbUNvt/MrPmivUeVpP5elvQZikmmXk8xUuYvKIYGNuoK4ILy5wuA7+5DGWZmzdfGfdzZjs5TI+LlwMaIeB/wJOCRw71B0qXAL4BHSVoh6VXAh4FnSroLeEb53Mys7bTzmpPZrpId5b/bJc0DNgBzh3tDRJw/xEtnJPdpZtY6Y6CP+3uSZgD/ANxKcUifa1qtzMxaqcVdIfVkR5V8oPzxcknfAzoiIj9Gy8ysQsQYGA4IIOlUilT18eVzIuKSJtXLzKylKt9wS/oy8AhgCQ/NVRLAqDTcMydt59yjf103bsuC/CT2q3bkJ3G/f0suUWDt+unpMg9YPzEd27EulyySTRQCmP3Zn6dj9zz7CenYjvW5+92NTKLfSALKxDk76gcBO2dOS5fZsTGfgDKpgXOwYlPue3XCjOXpMg+euSUdu3F2LgGnc1l+gZDJDSShrd6Q2z/AtsPqL6Qy4qrecFNkTB4bEW18KGZmI6iNW7vscMA7gEOaWREzs7aRGArYtsMBJV1J8XtnOvAbSTey99Jlz2tu9czMWqSNr7jrdZVcQTER1E8HbH8KsOqPw83MxoZ2Tnmv13CfA7wjIvaayk1SN/D3FAssmJmNOVUeVXLwwEYbICJul7SgKTUyM2u1iifgDDdeKT/5tZlZ1bRxw11vVMnNkv5q4EZJr6ZYf9LMbMzpz5ys5KgS4CLgO5JeykMN9UnAROD5zaxYrQd7JnLThsPrxh02NZ+Ff8y0/FTgx07P3YfdNS+/+smanflknWXbZqbiJj3zvnSZG/7q1HTsjHt21Q8qZVdAySafQGMJKIckE1A2zMon4MR9rU1A2TY/n3xyxPT82tur5uRG+PZMzq+WNHFLfrWg8Q2sFrR6Zz5ha6Sor30vuYdtuCNiDXCqpKcBx5Wb/ysirm96zczMWqXifdwARMQPgR82uS5mZm2jyqNKzMwentxwm5lVi6+4zcyqxg23mVmFtPkq7264zcwGGDMr4LTSnq0TeeD6+XXj7p1zaL7QrvzY5K5Z21JxR3Tmx9Ae0pGf8H71M3Pj03dduyBd5s7r0qENjWPu2Jj7tjc0iX4D45jnT9uUils5Z9i1rvfS6nHMjYxhnjc5d/wAvV27U3G7Dswv+jF1VX7RiY51+ebn/q35cf8jpo2XH6hEw21mNtp8xW1mViVjIQHHzOzhxjcnzcwqxg23mVmVBL45aWZWNb45aWZWNW64zcyqwwk4I2D8g8HBN9VPFuiZMi5d5q4ZHenYHbNyq7T9as6cdJlHvuPn6dhH35xLgNi0J58AtKKRBJQGPtdsAsr4tflJ9B/YkU++OGxK7jPIJp9AMxNQcnHLtuQW0gA4emp+gZBZXbnEsp2zZqfLnPZAvrXraGDRibXdnenYERFR3YUUzMwettq33XbDbWY2GHeVmJlVSQDuKjEzq5j2bbdb03BLug/YCvQCPRFxUivqYWY2FHeVDO5pEbG+hfs3MxuSR5WYmVVJm88OmJ8hfmQF8H1Jt0haNFiApEWSbpZ0857dD45y9czs4axIwIm6j1Zp1RX3kyNipaSDgGsl/TYiflIbEBGLgcUA02bNj10z61e1kdVHpi/vScdOW5FbAWb8D25Ol3nvh05Nx87Y+ftU3BFTu9Nl9jUrAeWBXAJKRwOdZMsbWP3kkdPWpOKyySfQ+gSUtd3T02XuOSSfLDW/M7dazp2z88ffOzF/LdixMT/9Xt+6/CpII6aNZwdsyRV3RKws/10LfAc4uRX1MDMbSjtfcY96wy1pqqTp/cOIx4cAAAqhSURBVD8DzwLuGO16mJkNKZKPFmlFV8nBwHck9e//axFxdQvqYWY2BM9VspeIuAc4frT3a2bWEC+kYGZWIeGly8zMqsdX3GZmFdO+7bYbbjOzwaivfftKKtFw7+kMVj29/oc4cV1+VZVJDSSAHPJPudVqep6RnytrcnL1E8ivgJJNPgGY3bU1HbtzVlc6dtrK3GVKY6ufjHwCSjb5BODOriYloGzKNQyxPp98sm73tHTs3MmbU3G3zckntu2Z1sBqSZvzSXCT1ueTwEZE0NYJOJVouM3MRpNobYJNPW64zcwG44bbzKxi3HCbmVWI+7jNzKrHo0rMzCol3FViZlYpgRvu/XXglB2cdeJtdeNW7TgwXea2p6xNx66+KLfowZzbd6XLbGQc8/ru3NjcPXPzY2gPb2Ac89LZ+XHc2XHM2THM0JxxzIdOyR//bXPy4413d+bPwaSNuXI71uXHMK94ML/oxImzlqfiJs3Zni5z56z8mPtG/g9MbsXqtO3bU1KNhtvMbLR5HLeZWdW44TYzq5AI6G3fvhI33GZmg/EVt5lZxbjhNjOrkAC85qSZWZUEhPu4zcyqI/DNyf3VF+LBnvpJGI0k1Uz76UHp2F0/zsU1Mon+pAYSUEgmoKzZ1ZkuMjuJPsCvDhr5BJRs8gk0loBy/7bcohNPmH1/fv9dO9Kxu2bkE1Amr08uOrEhXSQrNuYTcE6etSwVN29G/ruyZnb++OMepWM7NragEXUft5lZxbjhNjOrEk8yZWZWLQF4Wlczs4rxFbeZWZU45d3MrFoCwuO4zcwqxpmTZmYV4z7u/bP7t308cMqWunHzfplPQJk6voEElOQKKM1Y/QRgUjIBZcWD+RWAGkpAmZ1PQNk5M5eAkU0+AehoYPWTBzblPoNxs/N/Bs9tUgJK3725BJRGkk+6N0xJx245YnIq7vBp+dWCls05NB27Z2r+/8vEraPcbRHhUSVmZpXjK24zsyoJore31ZUYkhtuM7OBPK2rmVkFtfFwwPx0diNI0pmSfifpbklvb0UdzMyGEkD0Rd1HRr32TtIkSd8oX79B0oJ6ZY56wy1pHPCvwHOAY4HzJR072vUwMxtSlAsp1HvUkWzvXgVsjIijgX8EPlKv3FZccZ8M3B0R90TEbuDrwDktqIeZ2ZCit7fuIyHT3p0DfKn8+TLgDEnDjhVVjPKQF0kvBM6MiFeXz18GPDEiXjcgbhGwqHx6HHDHqFZ0dHQBDYxSroSxeEwwNo9rLB4TwKMiIj+gfhCSrqb4fOrpAHbWPF8cEYtryqnb3km6o4xZUT7/Qxkz5Llp25uT5cEvBpB0c0Sc1OIqjbixeFxj8ZhgbB7XWDwmKI5rf8uIiDNHoi7N0oqukpXA/Jrnh5XbzMzGmkx7978xksYDBwLDLljXiob7JuAYSUdKmgi8GLiiBfUwM2u2THt3BXBB+fMLgeujTh/2qHeVRESPpNcB1wDjgC9ExNI6b1tc5/WqGovHNRaPCcbmcY3FY4I2Oq6h2jtJ7wdujogrgM8DX5Z0N9BN0bgPa9RvTpqZ2f5pSQKOmZntOzfcZmYV09YN91hNjZd0n6TbJS0ZiaFLrSLpC5LWluNQ+7fNknStpLvKf2e2so6NGuKYLpa0sjxfSySd1co67gtJ8yX9UNJvJC2V9MZye2XP1zDHVPnzVU/b9nGXqaK/B54JrKC4O3t+RPympRUbAZLuA04aboB9FUh6KrANuCQijiu3fRTojogPl79sZ0bE21pZz0YMcUwXA9si4mOtrNv+kDQXmBsRt0qaDtwCnAtcSEXP1zDHdB4VP1/1tPMVt1Pj21xE/ITiLnit2vTdL1H8R6qMIY6p8iJiVUTcWv68FbgTOJQKn69hjmnMa+eG+1Bgec3zFYydkxLA9yXdUqb2jyUHR8Sq8ufVwMGtrMwIep2kX5ddKZXpThhMOfvc44EbGCPna8AxwRg6X4Np54Z7LHtyRJxAMWPYa8s/z8ecMomgPfviGvNp4BHAQmAV8PHWVmffSZoGXA5cFBF7LeRa1fM1yDGNmfM1lHZuuMdsanxErCz/XQt8h6JbaKxYU/Y99vdBrm1xffZbRKyJiN6I6AM+S0XPl6QJFA3cVyPi2+XmSp+vwY5prJyv4bRzwz0mU+MlTS1vpCBpKvAsxtbMh7XpuxcA321hXUZEf8NWej4VPF/lNKGfB+6MiE/UvFTZ8zXUMY2F81VP244qASiH8fwTD6WKfrDFVdpvko6iuMqGYsqBr1X1uCRdCpxOMf3lGuC9wH8C3wQOB5YB50VEZW72DXFMp1P82R3AfcBravqFK0HSk4GfArcD/SsAvJOiT7iS52uYYzqfip+vetq64TYzsz/Wzl0lZmY2CDfcZmYV44bbzKxi3HCbmVWMG24zs4pxw23DknSIpK9L+kOZon+VpEWSvtfCOv1I0rCL3Eo6RdJnJZ0uKSSdXfPa9ySd3sD+Tm/l8ZoN5IbbhlQmOHwH+FFEPCIiTgTeQTXms3gOcHX58wrgXS2si9mIcsNtw3kasCciPtO/ISJuo0h6mCbpMkm/lfTVspFH0nsk3STpDkmLa7b/SNJHJN0o6feSnlJuv1DStyVdXc4J/dH+fUl6lqRfSLpV0rfKOSmoeX2cpC+W+7pd0ptqXj4D+EH5823AZknPHHiAks6Q9Kvy/V+QNKncfmZ5bLcCL6iJn1rG3Vi+75xy+2PKbUvKyY2O2feP3Wx4brhtOMdRzHE8mMcDFwHHAkcBp5XbPxURTyjnsp4M/FnNe8ZHxMnl+95bs30h8CLgscCLVEyQ3wW8G3hGOSHXzcD/G1CHhcChEXFcRDwW+A+A8r17ImJzTewHy/L+l6QO4IvAi8r3jwf+utz+WeBs4ETgkJq3vYtiFe6TKX6x/UM5dcH/Af45IhYCJ1Fc5Zs1hRtu21c3RsSKciKfJcCCcvvTJN0g6Xbg6cBjat7TP7HRLTXxANdFxOaI2An8BjgCOIXil8L/SFpCMY/GEQPqcA9wlKRPSjoT6J/t7lnA92sDy3m2+9Ok+z0KuDcifl8+/xLwVODR5fa7yhnzvlLznmcBby/r9COggyJd/BfAOyW9DTgiInYM8pmZjYjxra6AtbWlwAuHeG1Xzc+9wPjySvXfKFb3Wa5i5ZiOQd7Ty97fvT8qCxBwbUScP1TlImKjpOOBZ1Nc8Z4HvJKif/sTg7yl/6q7Z6gyEwT8eUT8bsD2OyXdADwXuErSayLi+v3Yj9mQfMVtw7kemFS72IOkxwFPGSK+v5FeX/ZHD9XoZ/wSOE3S0eV+p0p6ZG1A2SVyQERcTtEgn1D2qT+O4q+AvUTE94GZ5esAvwMW9O8DeBnwY+C35fZHlNtrf3lcA7y+pu/+8eW/RwH3RMS/UMyw9zjMmsQNtw2p7CZ4PvCMcjjgUuBDFCulDBa/iaJv+A6KBu6m/dj3Oor1EC+V9GuKrohHDwg7FPhR2W3xFYoRLycCv4qhZ0/7IOU872XXzCuAb5VdO33AZ8rti4D/Km9O1s5R/QFgAvDr8vP4QLn9POCOsi7HAZfs67Gb1ePZAW1MkfRuirVKv97qupg1ixtuM7OKcVeJmVnFuOE2M6sYN9xmZhXjhtvMrGLccJuZVYwbbjOzivn/li3L6sjMWncAAAAASUVORK5CYII=
"
>
</div>

</div>

<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAW4AAAEWCAYAAABG030jAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADh0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uMy4yLjIsIGh0dHA6Ly9tYXRwbG90bGliLm9yZy+WH4yJAAAgAElEQVR4nO3deZhcVZnH8e+bfScJgewkJCwaAoSdEEF2UQRkRJBhFFQMo+IGM4LKCCqooOi4jEsQRFxYBIGAsi8BAiYkIUDCFkiCJGTf96Xzzh/3tKk0XV1vJ11ddZvf53nq6a5bb5177lKnbp17FnN3REQkP1pVOgMiItI4KrhFRHJGBbeISM6o4BYRyRkV3CIiOaOCW0QkZ3JTcJvZOWb2YDD2PDN7qox5KWv628PMHjez85sgndlmdvx2vrejmd1jZivM7C9p2ZVmttjM5pvZYDNzM2uzHWlv93vrpLPazIY08Pp2b7+UZmY3mtmVlc5Hfczsc2a2IJ0jO1c6Pw0pa8FtZl83s/vqLJtRZNnHG0rL3f/k7ic2Ub6apJBrIP12ZvYtM3vVzNaY2Vwzu8/MmiT/VewMoDews7t/zMx2Ay4Ghrl7n8pmLePuXdx9JlR3ISLNy8zaAj8GTkznyJJK56kh5b7ifgI4wsxaA5hZX6AtcECdZXuk2JbiduA04JNAD2B34KfAyfUF7+hVZBUZBLzm7pvT892AJe6+sIJ5yoVqPAeqMU/bK7AtvYEOwPRmyM6Oc/eyPYB2wFrgoPT8TOB3wLg6y15P/+8EXA/MA+YCVwKt02vnAU8VpH0i8CqwAvhlSvP8wljgR8AyYBbwwfTaVUANsB5YDfwiLX8P8BCwNKV7ZsG6dgbGAiuBicB3C/NSZ5uPB9YBA0rsm9nAJcALwAagDXAp8AawCngJOL0g/jxgPPCLtM2vAMcVvP54ytf49P4HgV5F1t0LuBdYnrb3SaBVQb7+K+VrBXAr0KG+Y5CWOdkX77eBjcCmtF8vSPthS3p+IzA4xbcJHO/W6fgtBmYCXyh8b508fAq4p+D5DOAvBc/fAkbUye/olNeNKX/3lNr+etbbCrgMeBNYCNwE7JReOxqYU88xPz79fwXZF/wfyc6r8+tJf6eU5qK0jssKjtObbP0MnZO2a5/0/DPAXQXruS2ls4qsYDq4gfPS076eAcxKy36a9uFKYDJwZEF8g+kDBwBT0mu3ArcAVxa8/lngdbLzcCzQr05ePp/ysors/B4KPJ3ychvQrsh2nEf2WfgJsITs3GpPdk79E1gA/BroCOwFrEnrWw08Ws5ysUnK1rKvAB4Dvpr+/wXwabLCs3DZDen/O4HfAJ2BXckKyQvqFhpkBc9K4N/ICrwvk30ICwvuTemkaA18DngbsPT64xR8UNL63iIrANqkk20x2U980sl2W4obTlbIFCu4fwA8Htgvs4GpwECgY1r2MaAfWYFwVjqZ+hZs02bgq2S/Ws4iK1h6FmzTG+kk7Jie/6DIur+fTtq26XFkwb6ZnfZ7P6An8DLwn3WPQZ0P1x4FH+I/Frx2NAWFF+8suBs63v9J9uU0MOXjMYoX3EPIvoRapXy/Wbve9NoythZ4hfm9kYJCpNT217PeT5MVOkOALsBfgT/Ut+0FaRcW3JuAj6R8d6wn/ZuAu4Guad+9Bnym4LWL0/9j0rH/XMFrXy1Yz3rgQ2Sfhe8D/2jgvHSyC5iebD0v/4Ps4qUNWdXXfLZ+mRdNn+zC7U22nrNnpG2+Mr1+LNnn7ECyQvXnwBN18nI30A3Yh+wC55G0v3ciu7g5t8h2nEf2efliyndHskJ8bNq2rsA9wPfrOzer/dEcBfcVwJ3p/+eBPYGT6iw7l+ynyobCExg4G3isbqFBVgXxTEGckRW8hQX36wWvd0oHpU96/jjbFtxnAU/WyfdvgMvTybgJeE/Ba9+jeMH9W+CWguc9yQqVFcD6Oh/iT5fYd1OB0wq26V9fPmnZROATBdt0WcFrnwfuL5Lud9IHYo96XpsN/EfB82uAX9c9BgWvb1fBHTjej1JQYJL9wir6wUrH/0Dg42QF2USyX1GfAsYWye+N1F9w17v99azzEeDzBc/3TudKm7rbXpB2YcH9RH3pptdbk/0aGFaw7ALSRQHZVfXY9P/LwPm15x1ZYXlgwXoeLkhjGLCugfU6cGyJ83IZsH+p9IGjeOc5+zRbC+7rgWsKXuuS9t/ggryMKnh9MnBJwfNrgf8tksfzgH8WPDeyC6GhBctGsvVXxeCGzq9qezRHq5IngPeZWU9gF3efQXbwjkjLhqeYQWTfyvPMbLmZLScrPHetJ81+ZB9UADzb83PqxMwveH1t+rdLkTwOAg6rXW9a9zlAH2AXsg/iWwXxbzawvUuAvgXrXuru3YGDyK4qChWmiZl90symFuRhONmvi1pz07YW5qNfwfP5Bf+vpfj2/pDsSvFBM5tpZpfWeT2azo4odby3OcY0vM8hqyo7mqywGEf2Rfb+9BjXyLxFt7/26r4wj7VfShFvNfBaL7L9Uzf9/un/ccCR6R5Ra7JfhKPMbDDZ1ejUgvfV3Z4OJep8656X/2VmL6fWQstT+oXnZbH0+1H/OVtrm/3n7qvJPj/9C2IWFPy/rp7nDZ2bhduxC9kF3OSC8+3+tDx3mqPgfobsQH+WrM4Jd19J9k38WeBtd59FtpM3kNXLdk+Pbu6+Tz1pzgMG1D4xMyt8HuB1nr8FjCtYb3fP7ix/jqx+cTPZT/ZauzWQ9iPAIWYWyc+/8mFmg4DrgAvJWmV0B6aRXSnU6p+2tTAfbwfWs+1K3Ve5+8XuPgQ4FbjIzI4LvHUN2clfm+cdaSlS6njPI77PYWvBfWT6fxylC+6650FjvU32BVRrN7JzZQHv3FeteWch0dD6F5NdfdZNfy6Au79OVkh+kezKfSVZATqa7FfRlu3Ynnfky8yOBL5Gdi+qRzovV7DteVnMPOo/Z2tts//MrDNZlczc7c/6Ngr372Kygn6fgvNtJ3cvx0VJ2ZW94Hb3dcAk4CKym2C1nkrLnkhx88huqF1rZt3MrJWZDTWz99eT7N+Afc3sI+mb/QtkV8dRC8jqyWrdC+xlZp8ws7bpcYiZvdfda8jqLq8ws05mNoysaqfY9j5IVh97l5kdlpoGtgUOL5GnzmQn2iIAM/sU2RV3oV2BL6X8fQx4L/D38FYnZvZhM9sjfaBWkN2sjXzQnwf2MbMRZtaB7Gfydgkc79vItnWAmfUgu3HbkHHAMWRVL3PIzrWTyAqC54q8p+550Fg3A181s93NrAtZFdqtnrWqeY3syvPkdPwv452/uIpK591twFVm1jV9sV9EdjOz1jiyL/raL6bH6zxvCl3JvowWAW3M7Ftkdc4Rz6T31p6z/wYcWvD6zcCn0vnUnmz/TXD32U2W+yR9kV0H/MTMdgUws/5m9oGmXldzaK4OOOPICp3CTitPpmWFzQA/SXZD4yWyerTbKah2qOXui8lu5F1D9tNqGNmXw4Zgfn4KnGFmy8zsZ+6+iqwO9eNkVwHzgavZ+kG7kOwn2XyyetHflUj/dLIvgz+S1W/PIqt6KXqSuPtLZHV2z5AVKPuSfqEUmEB2j2Ax2Q3eM3z72pvuCTxMdgf9GeCX7v5YqTe5+2tk9eMPk93p39FOSA0d7+uAB8i+LKaQfXmWyttq0sVBugKdCYxPhWB9rgeGpZ/Od21H/m8A/kB2Ds8iu0n3xbT+FWT3GX5LdgW5hndW55XyxfS+mWT7+s9pnbXGkRWsTxR53hQeIKtSeI2sWmM9DVfx/Iu7byRrQHAeWauRsyg4ju7+MPA/wB1kV+dDyT6D5XIJWRXhP8xsJdl5vHcZ11c2tS0Jcs3MWpF9KM6JFEB5ZGbnkd1QfV+l8yIilZWbLu91mdkHzKx7+on1DbI6t39UOFsiImVXtoLbzAaa2WNm9pKZTTezL6flV6Qu4FPT40PbuYqRZG1XFwOnAB9J9ekiIlXDzG4ws4VmNq3I62ZmPzOz183sBTM7sGSa5aoqSc2U+rr7FDPrStYG8yNkd6dXu/uPyrJiEZEqYmZHkd1/ucnd6zY4IF28fpGsE9NhwE/d/bCG0izbFbe7z3P3Ken/VWSdBPo3/C4RkZbF3Z8guzlbzGlkhbq7+z+A7unCt6hmGUQmdQo4gKxVxCjgQjP7JFlLkIvdfVk97xlN1iYVa9fuoHa96uuHs60e3VeH87Rmc7twrC9oGwwMJ9konfqvLR0ErH27U+mgpH3f9eHY9Qs6hmNtl02huC5tog2AYMXCeFPbnXaNnQPLNsT3VdtFkSbLmfb94vt13eLYfm21KX5itemzMRzboXXsWK2e0zmcpreK7yvbEt8uWxn7DACsYtlid9+hjjUfOKazL1larDHSVpNf2DCdrKVNrTHuPqaRq+vPti115qRl84q9oewFd2rfegfwFXdfaWa/IhssxtPfa8nGfNhG2vgxAB36D/TdPn9RyXV97JQnS8bUmrh0UOmgZMOP+5UOonEfMG/Eb50RVxZrhrytKd8uWTX2L3t886Vw7GvXvOPXXVHtPhfrD3REr1nhNO/7vyPDsR/8QuwcuOP1EeE0+4wJN79m0HdeC8dO+21sv3aev7l0ULLzJbPDsXt3XVA6CHjm0kNLByU1HeIndusN8T5C7e57Nhz7sN9eqpdtSUuW1jDxgVJ9vqB13xnr3f3gHV1fY5W14E4dD+4A/uTufwVw9wUFr19H1t5ZRKRqOLAl1CetScxl217CAyjRe7ScrUqMrIPDy+7+44LlhXU3p5N16xYRqRqOs8lrSj6ayFjgk6l1yeHAitSzuKhyXnGPAj4BvGhmtQPefAM428xGkH2pzSYb8UxEpKo01RW3md1MNo5OLzObQzbqaFsAd/812bAVHyLr1bmWbETLBpWt4Hb3p6h/IJpGj60hItKcHKemiZpKu/vZJV53svGWwlrM1EQiIk1pS7maiTUBFdwiInU4UKOCW0QkX3TFLSKSIw5squKRU3NRcFvHGloPW1ky7q6b4x013v+xyeHYF74U6zm55Zele3fWWjmodTj2+a/HOovMOzZ+OO27w8Kxq4bGW412+0WDPXX/5d4B8QmLRl0QP1aPzIsNr7xpY3xfHXz1lHDs7eMPCccecO7robi5Y4aG04x2qgEYe9uoUFzNyHCSdD4oPjz8zh9+NRy78YPx/crfb4/HFuG4qkpERHLFoaZ6y20V3CIidWU9J6uXCm4RkXcwakLzIVeGCm4RkTqym5MquEVEciNrx62CW0QkV7boiltEJD90xd0Eurdfx78Nfb5k3PjfNDhN2zamT9s/HGvBJtdt18QHvF+/c7wdtwVvbw98JD77yT8/EJzVBzj12Anh2HHBY9D9jdjsKwDrauJ5nf92j1Dc4Fvjbb2euyQ+496RB70Sjm1lsTwsWRYfPnT85YeHYzt8NtbmutP13cNpdrw83jZ7yb2xNvcAnX5bthGo6+UYNeUb9XqH5aLgFhFpbqoqERHJEcfY6PFfxc1NBbeISB1ZBxxVlYiI5IpuToqI5Ii7UeO64hYRyZUtuuIWEcmP7OZk9RaP1ZszEZEK0c3JJrB0XSdunn5wybiR344NTA8w+f74RALtg2PDH3Xe1HCaW76xXzh28X7tQnEdlsY7lQy6L95Z529r4x2bjj0/NunAA0/HJocAaHXZe8Kxu/SPndJvnhzfV33GxDvgzPls/Of1ivUdQ3EHf2taOM3Xv/7ecGy71rGOPR3vjHfAWnd6/FxZMzne3K7r+niHraZSo3bcIiL5oZ6TIiI5tEWtSkRE8iMbZEoFt4hIbjjGJnV5FxHJD3fUAUdEJF9MHXBERPLE0RW3iEju6ObkDmq1rhUdXizdWWHWXfGOGv2WbgjHzjo1NgPL9Ev2Dad5+LXPhmPvfiOW7qJFncJpLhoZv/HS7+HgFDxA+5NjswC1778mnOass9uHY9t0WhuKO2HIjHCaj66Ldxbau028o8gRA2aF4qYsHxhOc2O3+Ee66wdjHdZW3bdHfP01y8OxrZ/eORw78gcTw7FP3BcOLcoxTaQgIpInDmzSWCUiInliGo9bRCRPHPWcFBHJnWq+4i7bV4qZDTSzx8zsJTObbmZfTst7mtlDZjYj/e1RrjyIiGwPd2OLtyr5qJRyrnkzcLG7DwMOB75gZsOAS4FH3H1P4JH0XESkamQ3J1uXfFRK2apK3H0eMC/9v8rMXgb6A6cBR6ew3wOPA5eUKx8iIo2nOScxs8HAAcAEoHcq1AHmA72LvGc0MBqgfYfu9Hm2dLvrQ6+dFM7TM9+MD/jurWOD7q/tHZvwAGDcD0aGY9edFGsb3XdwcMYHgBt3CYce883x4dhlm2NtyWtq4h+KXR+LtaMHOPbiWPv455fHJ0foud+icOz0l3eLx3bqF4o7fd/4BB3T7nw7HBud9KDTj2LnH0DbLvEi5cRvx8+rV1fVW0yUTXZzsnrruMtecJtZF+AO4CvuvtJs685wdzezektFdx8DjAHo1m1AfLoSEZEm8K7tOWlmbckK7T+5+1/T4gVm1tfd55lZX2BhOfMgItJY1d5zspytSgy4HnjZ3X9c8NJY4Nz0/7nA3eXKg4jI9tpCq5KPSinnFfco4BPAi2ZWW0n3DeAHwG1m9hngTeDMMuZBRKTR3GHTlndhVYm7PwVFW7AfV671iojsqKyq5F1YcIuI5Fk195xUwS0iUse7vjmgiEj+qKpkh21pY6zrVboTxm3TD4yn+bGacOzuf4x985rHOyrMuSA+4H7fbrFJB5Y/Ge+kcMolT4dj/zT+iHDs/vvODsUNHBM/9WZ+YmM4dsJ/HxKKW9Mn3qlnSyM+Ja32j3c5aDc/NkHEtHPj5+rwKfFu2K+sfCsUN7BTfHKEV74zPBz76LXx86rDsvg+aCqac1JEJEeyViWVG4ukFBXcIiJ1VHsHHBXcIiL1UFWJiEiOqFWJiEgOqVWJiEiOuBubVXCLiOSLqkpERHJEddxNoKY9rBha+mfLKe95MZzmc0sHhGPX79wnFNd+ebyTQLf7OodjFxwXa0+69wmzw2muq4nP1tNqffwn4+Kf7h6KW/3eeJrd4hPA8PaoWFzXN+MdZRYfGe8sNeCeeNvfjnfGOkG9dXm8o8qMF0vPFFXrnP0nhuLumzMsnOa+l70Sjl25qUM49p+/3yMc21RUcIuI5IjacYuI5JDacYuI5Ig7bH43TqQgIpJnqioREckR1XGLiOSQq+AWEckX3ZzcQa3XQ8+XS7eRfmzOnuE0e/2sUzi2VZtY++wFo9eF09yp0/pwbI87dg3FbTw73ob44bsODsd2XREOxS3WPnrEf0wLp/n6D+PtiFfFmpFTsyB+4+njBz4bjp386fiHfd3ph4XiNvbYEk6TtfGP9NTlsb4MO3WIn9eNqV547vngwQLef378fJlyXTi0KPcWUMdtZkOBOe6+wcyOBvYDbnL3+NQYIiK5YdRUcauSaM7uAGrMbA9gDDAQ+HPZciUiUmHuVvJRKdHfVVvcfbOZnQ783N1/bmbPlTNjIiKV0lLGKtlkZmcD5wKnpGXx2VZFRPLEs3ruahWtKvkUMBK4yt1nmdnuwB/Kly0RkcragpV8VEroitvdXzKzS4Dd0vNZwNXlzJiISKV4S7g5aWanAFOB+9PzEWY2tpwZExGpJPfSj0qJfqVcARwKLAdw96nAkDLlSUSk4lpCq5JN7r7CbJuMNqJXwI6p6QDL9irduaRHx3inlr5XzgvHPjMz1lHgkD7xNCdMiXcW2u2st0Nxw7vH118zsXc4dtQ1E8KxizZ2DcVN+fX+4TQP/fqUcOyRbWLnwN2LgjMuAJNHxD+gB02NX4bdMiXWsavXk/F2AK0+tiQc++o/Yuf1Ls/FP+pvj45v/xmj4h2bJl1yYDi2KWRX1PlvVTLdzP4daG1mewJfAmLTd4iI5FA1NweMVpV8EdgH2ADcDKwEvlKuTImIVFo113FHW5WsBb6ZHiIiLZpjbKniViUNFtxmdg9ZJ6J6ufupTZ4jEZEqUMX9b0pWlfwIuBaYBawDrkuP1cAbDb3RzG4ws4VmNq1g2RVmNtfMpqbHh3Ys+yIiZeA5blXi7uMAzOxady8cB/QeM5tUIu0bgV8AN9VZ/hN3/1FjMyoi0qyq+JI7WonT2cz+1W47dXnv3NAb3P0JYOkO5E1EpGJye8Vd4KvA42Y2EzBgEDB6O9d5oZl9EpgEXOzuy+oLMrPRteto263Hdq5KRKTxHNiypXqbA0Zbldyf2m+/Jy16xd03bMf6fgV8l2y/fJes/vzTRdY5hmzsb9oPHuBr9tpUMvENk/uGM9Lu4Z7h2FOueT4UN3vNzuE0z3zfP8Kxdzw8MhR3+PGzw2nudeVL4dh73hwejl37SvdQ3M6NOHuWbOgSjn1yztBQ3IAr490Q5lx2RDh28W/CofRaH/st3mpzPM2dO60Jx444dm4o7qGO+4XTHHR1vGPXnef1Cse2Hd2IE+aBeGhRDlRxO+7oDDhtgQuAo9Kix83sN+5eujQt4O4LCtK8Dri3Me8XEWkuLWFY118BBwG/TI+D0rJGMbPCS+LTgfhEciIizckDjwqJ1nEf4u6Fg0s8amYN1h+Y2c3A0UAvM5sDXA4cbWYjyDZ5NtlVvIhIlanszcdSogV3jZkNdfc3AFILkwZHyHH3s+tZfH0j8yciUhlVXFUSLbj/G3isTquST5UtVyIileTgLaBVySOpVcneadGr29mqREQkJ3JacJvZUUVeOszMajvZiIi0PDmuKvnvepY5sB8wECg9u4GISB7lteB291MKn5vZKOAyYD7ZGN3NokvHDYwaNqNk3Ma9o1X28Gz3WEcNAL9kRChu6PdeDqe5yePfebs9EGsuv/z9ncJp7tJuVTi218/i6a7YPfbzct2Z9XaYrde0u/cuHZT0uybWsWb+XcPCaZ42eHw49tZxsc5SAO2WxVrj9hu/MZzm/t1jnWoAbn8ldl73ei5eZTD7rHhsnx7xc/C4vq+GY78XjmxAC+mAcxzwP2Sb8z13f6isuRIRqbBq7oBTqo77ZLLJE1YAl7n7U82SKxGRSstxq5J7gDnAEuBrZva1whc1kYKItFSW1ytu4JhmyYWISDWpcJf2UkoV3OcA9wEPu3v8ToKISK5ZVd+cLHVb+3pgf+DvZvaImV1iZvuXeI+ISP7ldZApd58ATACuMLOdgROBi81sP2AKcL+731b+bIqINLMtlc5AceGGz+6+BLg5PTCzg4CTypSvbbRrtZnBHZeUjLv9riPDaQ54vsExsrZxxI8mhOIa0zb7rr/FB+fvEmxy/uzvYu1yAdqviF8uLD4h/pOxy1uxuOMGvhZOc9o18WP19tdi+3X4LvF2wSs3dwjH9mtEX+JVA2Nxs86JH6s118bPq83HxPoHdJkbH3Z/+PBXwrEdW8fTve//4p9tuLMRsUVUeTvuUA8AM/uymXWzzG/NbArQy92vKnP+REQqwrz0I5SO2Ulm9qqZvW5ml9bz+nlmtsjMpqbH+aXSjE6k8Gl3X0lWVbIz8Ang+8H3iojkTxPUcZtZa+D/gA8Cw4Czzay+bru3uvuI9PhtqXSjBXftb4YPATe5+3SqeegsEZHqcCjwurvPdPeNwC3AaTuaaLTgnmxmD5IV3A+YWVequupeRGTHBKtKepnZpILH6DrJ9AcK7/zMScvq+qiZvWBmt5tZybsf0ZuTnwFGADPdfW1qYaKJFESkZXKiXd4Xu/vBO7i2e4Cb3X2DmV0A/B44tqE3lBqr5MA6i4aYqYZERN4Fmqad9lyyIbBrDUjLtq4ma7FX67fANaUSLXXFfW0DrzklvhVERPKqicYqeRbY08x2JyuwPw78+zbrMevr7vPS01OBkuNDl+qAo7FKROTdqQkKbnffbGYXAg+QTTxzg7tPN7PvAJPcfSzwJTM7FdgMLAXOK5VudDzuTsBFwG7uPrp2/kl3v3f7Nqdxlq7pzJ8mBAaoHxyfBrPt+HiVz/1z3xuK6/KLncJpdh4UDmXFnrEz6KPHPRNO87Yph4Rjh/w5fh96U+dYJ6RpB8Y71QyfEu/YtOCt2AQNs3+5VzjNN9qHQ9nnv6eHY6f+cXgobsgf4ut/a/TacGyH1rHjOvvDncNpbrki9lkBWD60bTj2w194Mhz73JhwaMOaqEu7u/8d+HudZd8q+P/rwNcbk2a0VcnvgI1AbbesucCVjVmRiEheRFqUVHLY12jBPdTdrwE2Abj7WtSOW0Rasi1W+lEh0eaAG82sI+nHg5kNBeL1EiIiOZPniRRqXQ7cDww0sz8BowhUoIuI5FbeC253fygNLHU4WRXJl919cVlzJiJSKRWuwy4lPKwr0AFYlt4zzMxw90YMYikikiN5L7jN7GrgLGA6W8cocUAFt4i0SFbFozFFr7g/QtZuWzckRUQqLFpwzwTaUqGWJJ07buCw4W+UjJt+597hNNfvHP863XJPr1Dc7NM3h9PstuvycOwut8U69ky676BwmkMaMbjj20fEe6AM/O7Tobj1px4aTvOx6+M1em2DZ+iS/eK/g4895vlw7LRr9gvHdvHYMeh6+Zxwmid0ip9XbS3WCWrDoPj+n/hS3eGNius6J94J6+nFu4djm0zeq0qAtcBUM3uEgsLb3b9UllyJiFRSC7k5OTY9RETeHfJecLv778udERGRqpL3gtvMRgFXAIPSewxwdx9SvqyJiFSG0TJalVwPfBWYDITuKJjZDcCHgYXuPjwt6wncCgwGZgNnuntsODcRkeZS5XXc0UGmVrj7fe6+0N2X1D5KvOdG4KQ6yy4FHnH3PYFH0nMRkerTBLO8l0u04H7MzH5oZiPN7MDaR0NvSL0ql9ZZfBrZfGqkvx9pXHZFRJpJFRfc0aqSw9Lfwkkxt2fqst4FU/TMB3oXC0yzJY8GaN+hOwuvKN2Oc8P5a8IZWXdg9DsLdnqsYyiu266rw2ke3Pef4djZi94Tipv7uY3hNPte1yEcG22bDfDW/xxROgjo93S8S8DqgfF2xLs9FEt30ynxCQd2abcqHLumb/y8WjU49smf++LgcJrDR8WP1WNXjQrFLd43vk0nXzAhHPvI7w8rHZR0/VW/cGxTqeaqkmirkiafwjFo4F0AABDuSURBVMzd3az4rnH3McAYgK47DajiXSgiLVIVlzrhSxkzOxnYh2ywKQDc/TuNXN+C2okxzawvsLCR7xcRKT+v7lYlod9AZvZrskGmvkjWUuZjZE0DG2sscG76/1zg7u1IQ0Sk/Kq4jjtaeXWEu38SWObu3wZGAg3OtmpmNwPPAHub2Rwz+wzwA+AEM5sBHJ+ei4hUnWqeczJaVbIu/V1rZv2AJUDfht7g7mcXeem44DpFRCqnBdRx32tm3YEfAlPINum3ZcuViEglVbgqpJRoq5Lvpn/vMLN7gQ7uvqJ82RIRqRyjBTQHBDCzI8i6qrdJz3H3m8qULxGRisp9wW1mfwCGAlPZOlaJA81ScLftu5Fel88uGffWkw3eL93GwUe9Go59oXdsgoa9epYaBWCrmVe8Nxzb5ZuxgfQ3PTc4nGbbB54Jx276wCHh2GjHmpn/Hu/U0eeR+Cdo5LUTQ3GLNnYNpzn+a/GOIhvj80Nw8vsnh+I6to53rHr0B7FONQDzjo+1dxty26ZwmmM7xXdA/zfiE48M/Z+XwrFP3x4ObVjeC26yHpPD3L2KN0VEpAlVcWkXveyZBvQpZ0ZERKpGoClg1TYHNLN7yL53ugIvmdlEtp267NTyZk9EpEKq+Iq7VFXJWLKBoJ6ss/xIYN47w0VEWoZq7vJequA+Dfi6u79YuNDMlgLfI5tgQUSkxclzq5LedQttAHd/0cwGlyVHIiKVlvMOON0beC02SLWISB5VccFdqlXJJDP7bN2FZnY+2fyTIiItTm3PyVy2KgG+AtxpZuewtaA+GGgHnF7OjBXauKg9b/1yz5JxZ32t7j3U4h768fvCsaddND4U9/Si0rP01FrbJz6ry8jub4fiNn41fr/4jZ+MDMe2HRif2af/r9qF4s488Nlwmg9Nis2qA/GONd3bxmfA2f/7U8Ox05Y3OPbaNl5f3SsUN/uhweE0u5+3IBzL7J1DYasGxo4pwG4PxDvrvHVcPF2/alg4tqnYluq95G6w9HD3BcARZnYMMDwt/pu7P1r2nImIVErO67gBcPfHgMfKnBcRkaqR51YlIiLvTiq4RUTyRVfcIiJ5o4JbRCRHqnyWdxXcIiJ1tJgZcCrJapy2q2tKxo298chwmr5LfP03T4wNpP8fh8YnJ7hln3h738kjLBR30NT4mdZu+exw7Nqr+sdje7cNxd3xSLwd+U6NuPKZ8Y1Ye99/fiCWT4D+I+Lt49fc2i8cu+zodaWDgN5Hxttmz5vfIxzbcZdYW/b1PbuF0+wSm/MDgAGPxieIaExb+qfujuehQVU8/UAuCm4RkeamK24RkTxpCR1wRETebXRzUkQkZ1Rwi4jkiaObkyIieaObkyIieaOCW0QkP9QBpwls6mwsOKR0VtvGx/tn8yGrwrG7j2kfCzw0vv4h/xXvrDPzR7HOKst+Gl9/5/mbw7FDrnw5HDtp3m6huG73NzQr3rZWDwyH8v4LngvFHWKlO3TVuu2pw8OxfT66MBzb87ZYL7AlH4znte/98Y/0+y99x3Sy9frHbw4Jpzn3qPjkCB2WhEOZetkB8WBuaURsEe75nUhBRORdq3rLbRXcIiL1UVWJiEieOKCqEhGRnKnecrsyBbeZzQZWATXAZnc/uBL5EBEpRlUl9TvG3RdXcP0iIkWpVYmISJ5U+eiArSq0XgceNLPJZja6vgAzG21mk8xsUs2aNc2cPRF5N8s64HjJR6VU6or7fe4+18x2BR4ys1fc/YnCAHcfA4wB6LZ3bx806p8lE11wd6zzB4A90zUcu3jfWNzEEa3DaR46Nd6p4lCeCsU9uf/QcJrd28dmX4F4pxqAlQu7hOIGv7kpnOYJFzwbjl26qXMobtH6WD4BDjtwRjj2hfnxmY16vx3rBNXtN/HZetb2js2WBDDx4titpX2vfiGcZqtLgh8WYGPXePFTkZH6qnh0wIpccbv73PR3IXAnjepzKCJSftV8xd3sBbeZdTazrrX/AycC05o7HyIiRXnwUSGVqCrpDdxpZrXr/7O731+BfIiIFKGxSrbh7jOB/Zt7vSIijaKJFEREcsQ1dZmISP7oiltEJGeqt9xWwS0iUh/bUr11JbkouM2gXavSHVZab4ynuXLPeAeYPS+cEIqbd/ER4TTHfy2e2VlnxFptnn1oLJ8Ad98+KhzbcUE4lJ7BPkirL4wPU9O2EbPVvPGN94bi9rt6ajjNe16JdyrZ7ab4R2pD99jO6rAkfuk3/4h4YWM1sY49S26MjwHXrXN8ZiU+H58taMvPYrMFNRmnqjvg5KLgFhFpTkZlO9iUooJbRKQ+KrhFRHJGBbeISI6ojltEJH/UqkREJFdcVSUiIrniqODeUW1sS2jg/7Uz4m2je/1qUjh2xi8OC8V1mRVOknmjN4RjuwYnfXj0qXg78v0ueDUcO+nN+EQKu45tH4rr8L/dwmmO6xLfrjkfjcXZ1+LjnI288o1w7LzN8cks2p6/KBQ3a+7O4TQH/SVe2LReH2tz/fb7YscUoFUjPgP79Hw7HDvjovjEG9wTD21Q9daU5KPgFhFpbmrHLSKSNyq4RURyxB1qqreuRAW3iEh9dMUtIpIzKrhFRHLEAc05KSKSJw6uOm4RkfxwdHNyR61d1oHn7xhWMq7vw0+H09x8fHxw+B7TYwPe17QLJ0mbZ2OdagCi8wiccNFT4TRvve/IcGyrIWvCsasGxCZ9mHdS/Gdo+9nB2RmAQ/Z9LRT33PK9wmluXNUjHLvyS2vDscf0nBOKm7Mwvv6RV8U7lj1x1chQ3EEnvRROc+4ze4Rjx/3loHDsR85+Mhz7cDiyBNVxi4jkjApuEZE80SBTIiL54oCGdRURyRldcYuI5Im6vIuI5IuDqx23iEjOqOekiEjOVHEdt3kVZ65WN+vph9lxJePm/Vd8ppT9PxrvVLB8Q8dQ3MYt8Y4ib46PzyrT+9nYTCWbusTXP/DzM8Kxi789OBy76xWxKVAmTIvPFHPOYc+EY2evi80WM/6lPcNpdn6tbTi2x2vB3lLA0vfGjtdOb8R/sndcHJ8pZv4hsZlt1u9bevapWmfvE+8A9Nc34rMQ1bwUnzFpxmUXTXb3eA+7euzUupeP7HJqybgHVv5uh9e1PXTFLSJSnyq+qFXBLSLyDo7XxH89NTcV3CIidWlYVxGRHKri5oCxodyamJmdZGavmtnrZnZpJfIgIlKMA77FSz4iSpV3ZtbezG5Nr08ws8Gl0mz2gtvMWgP/B3wQGAacbWalx2wVEWkuniZSKPUoIVjefQZY5u57AD8Bri6VbiWuuA8FXnf3me6+EbgFOK0C+RARKcprako+AiLl3WnA79P/twPHmZk1lGizt+M2szOAk9z9/PT8E8Bh7n5hnbjRwOj0dDgwrVkz2jx6AYsrnYkm1hK3CVrmdrXEbQLY293jM5XUw8zuJ9s/pXQA1hc8H+PuYwrSKVnemdm0FDMnPX8jxRQ9NlV7czJt/BgAM5tUiUbu5dYSt6slbhO0zO1qidsE2XbtaBruflJT5KVcKlFVMhcYWPB8QFomItLSRMq7f8WYWRtgJ2BJQ4lWouB+FtjTzHY3s3bAx4GxFciHiEi5Rcq7scC56f8zgEe9RB12s1eVuPtmM7sQeABoDdzg7tNLvG1MidfzqiVuV0vcJmiZ29UStwmqaLuKlXdm9h1gkruPBa4H/mBmrwNLyQr3BuVikCkREdmqIh1wRERk+6ngFhHJmaouuFtq13gzm21mL5rZ1KZoulQpZnaDmS1M7VBrl/U0s4fMbEb626OSeWysItt0hZnNTcdrqpl9qJJ53B5mNtDMHjOzl8xsupl9OS3P7fFqYJtyf7xKqdo67tRV9DXgBGAO2d3Zs909PgNClTKz2cDBDTWwzwMzOwpYDdzk7sPTsmuApe7+g/Rl28PdL6lkPhujyDZdAax29x9VMm87wsz6An3dfYqZdQUmAx8BziOnx6uBbTqTnB+vUqr5iltd46ucuz9Bdhe8UGH33d+TfZByo8g25Z67z3P3Ken/VcDLQH9yfLwa2KYWr5oL7v7AWwXP59ByDooDD5rZ5NS1vyXp7e7z0v/zgd6VzEwTutDMXkhVKbmpTqhPGn3uAGACLeR41dkmaEHHqz7VXHC3ZO9z9wPJRgz7Qvp53uKkTgTVWRfXOL8ChgIjgHnAtZXNzvYzsy7AHcBX3H1l4Wt5PV71bFOLOV7FVHPB3WK7xrv73PR3IXAnWbVQS7Eg1T3W1kEurHB+dpi7L3D3GnffAlxHTo+XmbUlK+D+5O5/TYtzfbzq26aWcrwaUs0Fd4vsGm9mndONFMysM3AiLWvkw8Luu+cCd1cwL02itmBLTieHxysNE3o98LK7/7jgpdwer2Lb1BKOVylV26oEIDXj+V+2dhW9qsJZ2mFmNoTsKhuyIQf+nNftMrObgaPJhr9cAFwO3AXcBuwGvAmc6e65udlXZJuOJvvZ7cBs4IKCeuFcMLP3AU8CLwK1MwB8g6xOOJfHq4FtOpucH69SqrrgFhGRd6rmqhIREamHCm4RkZxRwS0ikjMquEVEckYFt4hIzqjglgaZWR8zu8XM3khd9P9uZqPN7N4K5ulxM2twklszO9zMrjOzo83MzeyUgtfuNbOjG7G+oyu5vSJ1qeCWolIHhzuBx919qLsfBHydfIxn8UHg/vT/HOCbFcyLSJNSwS0NOQbY5O6/rl3g7s+TdXroYma3m9krZvanVMhjZt8ys2fNbJqZjSlY/riZXW1mE83sNTM7Mi0/z8z+amb3pzGhr6ldl5mdaGbPmNkUM/tLGpOCgtdbm9mNaV0vmtlXC14+Dng4/f88sMLMTqi7gWZ2nJk9l95/g5m1T8tPSts2Bfi3gvjOKW5iet9pafk+adnUNLjRntu/20UapoJbGjKcbIzj+hwAfAUYBgwBRqXlv3D3Q9JY1h2BDxe8p427H5red3nB8hHAWcC+wFmWDZDfC7gMOD4NyDUJuKhOHkYA/d19uLvvC/wOIL13k7uvKIi9KqX3L2bWAbgROCu9vw3wubT8OuAU4CCgT8Hbvkk2C/ehZF9sP0xDF/wn8FN3HwEcTHaVL1IWKrhle0109zlpIJ+pwOC0/Bgzm2BmLwLHAvsUvKd2YKPJBfEAj7j7CndfD7wEDAIOJ/tSGG9mU8nG0RhUJw8zgSFm9nMzOwmoHe3uRODBwsA0znZtN+laewOz3P219Pz3wFHAe9LyGWnEvD8WvOdE4NKUp8eBDmTdxZ8BvmFmlwCD3H1dPftMpEm0qXQGpKpNB84o8tqGgv9rgDbpSvWXZLP7vGXZzDEd6nlPDduee+9ICzDgIXc/u1jm3H2Zme0PfIDsivdM4NNk9ds/ructtVfdm4ulGWDAR9391TrLXzazCcDJwN/N7AJ3f3QH1iNSlK64pSGPAu0LJ3sws/2AI4vE1xbSi1N9dLFCP+IfwCgz2yOtt7OZ7VUYkKpEWrn7HWQF8oGpTn0/sl8B23D3B4Ee6XWAV4HBtesAPgGMA15Jy4em5YVfHg8AXyyouz8g/R0CzHT3n5GNsLcfImWigluKStUEpwPHp+aA04Hvk82UUl/8crK64WlkBdyzO7DuRWTzId5sZi+QVUW8p05Yf+DxVG3xR7IWLwcBz3nx0dOuIo3znqpmPgX8JVXtbAF+nZaPBv6Wbk4WjlH9XaAt8ELaH99Ny88EpqW8DAdu2t5tFylFowNKi2Jml5HNVXpLpfMiUi4quEVEckZVJSIiOaOCW0QkZ1Rwi4jkjApuEZGcUcEtIpIzKrhFRHLm/wHyldj3CrE3zQAAAABJRU5ErkJggg==
"
>
</div>

</div>

<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>

Using networkx on a binarized graph: 


</pre>
</div>
</div>

<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Define-Small-Worldness-functions">Define Small-Worldness functions<a class="anchor-link" href="#Define-Small-Worldness-functions">&#182;</a></h2><p>Now we got everything to define our small-worldness functions.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[49]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">weighted_sw_sigma</span><span class="p">(</span><span class="n">matrix</span><span class="p">,</span> <span class="n">n_avg</span><span class="o">=</span><span class="mi">1</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Calculate the weighted small world coefficient sigma of a matrix.&quot;&quot;&quot;</span>
  <span class="n">sigmas</span> <span class="o">=</span> <span class="p">[]</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_avg</span><span class="p">):</span>
    <span class="n">random_graph</span> <span class="o">=</span> <span class="n">random_reference</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
    <span class="n">C</span> <span class="o">=</span> <span class="n">weighted_clustering_coeff_z</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
    <span class="n">C_rand</span> <span class="o">=</span> <span class="n">weighted_clustering_coeff_z</span><span class="p">(</span><span class="n">random_graph</span><span class="p">)</span>
    <span class="n">L</span> <span class="o">=</span> <span class="n">weighted_characteristic_path_length</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
    <span class="n">L_rand</span> <span class="o">=</span> <span class="n">weighted_characteristic_path_length</span><span class="p">(</span><span class="n">random_graph</span><span class="p">)</span>
    <span class="n">sigma</span> <span class="o">=</span> <span class="p">(</span><span class="n">C</span><span class="o">/</span><span class="n">C_rand</span><span class="p">)</span> <span class="o">/</span> <span class="p">(</span><span class="n">L</span><span class="o">/</span><span class="n">L_rand</span><span class="p">)</span>
    <span class="n">sigmas</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">sigma</span><span class="p">)</span>

  <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">sigmas</span><span class="p">)</span>

<span class="k">def</span> <span class="nf">weighted_sw_omega</span><span class="p">(</span><span class="n">matrix</span><span class="p">,</span> <span class="n">n_avg</span><span class="o">=</span><span class="mi">1</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Calculate the weighted small world coefficient omega of a matrix.&quot;&quot;&quot;</span>
  <span class="n">omegas</span> <span class="o">=</span> <span class="p">[]</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_avg</span><span class="p">):</span>
    <span class="n">random_graph</span> <span class="o">=</span> <span class="n">random_reference</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
    <span class="n">lattice_graph</span> <span class="o">=</span> <span class="n">lattice_reference</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
    <span class="n">C</span> <span class="o">=</span> <span class="n">weighted_clustering_coeff_z</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
    <span class="n">C_latt</span> <span class="o">=</span> <span class="n">weighted_clustering_coeff_z</span><span class="p">(</span><span class="n">lattice_graph</span><span class="p">)</span>
    <span class="n">L</span> <span class="o">=</span> <span class="n">weighted_characteristic_path_length</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
    <span class="n">L_rand</span> <span class="o">=</span> <span class="n">weighted_characteristic_path_length</span><span class="p">(</span><span class="n">random_graph</span><span class="p">)</span>
    <span class="n">omega</span> <span class="o">=</span> <span class="p">(</span><span class="n">L_rand</span><span class="o">/</span><span class="n">L</span><span class="p">)</span> <span class="o">/</span> <span class="p">(</span><span class="n">C</span><span class="o">/</span><span class="n">C_latt</span><span class="p">)</span>
    <span class="n">omegas</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">omega</span><span class="p">)</span>

  <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">omegas</span><span class="p">)</span>


<span class="k">def</span> <span class="nf">weighted_sw_index</span><span class="p">(</span><span class="n">matrix</span><span class="p">,</span> <span class="n">n_avg</span><span class="o">=</span><span class="mi">1</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Calculate the weighted small world coefficient omega of a matrix.&quot;&quot;&quot;</span>
  <span class="n">indices</span> <span class="o">=</span> <span class="p">[]</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_avg</span><span class="p">):</span>
    <span class="n">random_graph</span> <span class="o">=</span> <span class="n">random_reference</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
    <span class="n">lattice_graph</span> <span class="o">=</span> <span class="n">lattice_reference</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
    <span class="n">C</span> <span class="o">=</span> <span class="n">weighted_clustering_coeff_z</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
    <span class="n">C_rand</span> <span class="o">=</span> <span class="n">weighted_clustering_coeff_z</span><span class="p">(</span><span class="n">random_graph</span><span class="p">)</span>
    <span class="n">C_latt</span> <span class="o">=</span> <span class="n">weighted_clustering_coeff_z</span><span class="p">(</span><span class="n">lattice_graph</span><span class="p">)</span>
    <span class="n">L</span> <span class="o">=</span> <span class="n">weighted_characteristic_path_length</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
    <span class="n">L_rand</span> <span class="o">=</span> <span class="n">weighted_characteristic_path_length</span><span class="p">(</span><span class="n">random_graph</span><span class="p">)</span>
    <span class="n">L_latt</span> <span class="o">=</span> <span class="n">weighted_characteristic_path_length</span><span class="p">(</span><span class="n">lattice_graph</span><span class="p">)</span>
    <span class="n">index</span> <span class="o">=</span> <span class="p">((</span><span class="n">L</span> <span class="o">-</span> <span class="n">L_latt</span><span class="p">)</span> <span class="o">/</span> <span class="p">(</span><span class="n">L_rand</span> <span class="o">-</span> <span class="n">L_latt</span><span class="p">))</span> <span class="o">*</span> <span class="p">((</span><span class="n">C</span> <span class="o">-</span> <span class="n">C_rand</span><span class="p">)</span> <span class="o">/</span> <span class="p">(</span><span class="n">C_latt</span> <span class="o">-</span> <span class="n">C_rand</span><span class="p">))</span>
    <span class="n">indices</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">index</span><span class="p">)</span>
  <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">indices</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Measure-Small-Worldness">Measure Small-Worldness<a class="anchor-link" href="#Measure-Small-Worldness">&#182;</a></h2><p>Feel free to play around a little bit.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[50]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># generate a new graph</span>
<span class="n">graph</span> <span class="o">=</span> <span class="n">generate_graph</span><span class="p">(</span><span class="n">n_nodes</span><span class="o">=</span><span class="mi">20</span><span class="p">,</span> <span class="n">regularity</span><span class="o">=</span><span class="mf">0.15</span><span class="p">)</span>

<span class="c1"># plot it</span>
<span class="n">plot_graph</span><span class="p">(</span><span class="n">graph</span><span class="p">)</span>


<span class="c1"># now we can calculate the small worldness of this one</span>
<span class="n">small_world</span> <span class="o">=</span> <span class="n">weighted_sw_sigma</span><span class="p">(</span><span class="n">graph</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Small worldness coefficient: &quot;</span><span class="p">,</span> <span class="n">small_world</span><span class="p">)</span>


<span class="c1"># actually we can calculate the small worldness multiple times and see how much the random graph affects the outcome.</span>
<span class="n">small_world_list</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="n">weighted_sw_sigma</span><span class="p">(</span><span class="n">graph</span><span class="p">,</span> <span class="mi">10</span><span class="p">)</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">10</span><span class="p">)])</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">Multiple small world measures of the same network graph:</span><span class="se">\n\n</span><span class="s2">&quot;</span><span class="p">,</span> <span class="n">small_world_list</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Small worldness coefficient:  0.8355098348216147

Multiple small world measures of the same network graph:

 [0.88443673 0.86865593 0.87885048 0.88398869 0.87829326 0.87051095
 0.88301246 0.87995413 0.86354839 0.88236722]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>As we can see, the small worldness measure has quite some variance in it. We should probably calculate it multiple times and average!</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Other-Graph-measures">Other Graph measures<a class="anchor-link" href="#Other-Graph-measures">&#182;</a></h2><p>Define some other graph measures that are interesting.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[51]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">weighted_global_efficiency</span><span class="p">(</span><span class="n">matrix</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;The weighted global efficiency is closely related to the characteristic path length.&quot;&quot;&quot;</span>
  <span class="n">n_nodes</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
  <span class="n">min_distances</span> <span class="o">=</span> <span class="n">weighted_shortest_path</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>

  <span class="n">sum_vector</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">)</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">):</span>
    <span class="c1"># calculate the inner sum</span>
    <span class="n">sum_vector</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">1</span><span class="o">/</span><span class="p">(</span><span class="n">n_nodes</span><span class="o">-</span><span class="mi">1</span><span class="p">))</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">([</span><span class="mi">1</span> <span class="o">/</span> <span class="n">min_distances</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">]</span> <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_nodes</span><span class="p">)</span> <span class="k">if</span> <span class="n">j</span> <span class="o">!=</span> <span class="n">i</span><span class="p">])</span>

  <span class="k">return</span> <span class="p">(</span><span class="mi">1</span><span class="o">/</span><span class="n">n_nodes</span><span class="p">)</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">sum_vector</span><span class="p">)</span>


<span class="k">def</span> <span class="nf">weighted_transitivity</span><span class="p">(</span><span class="n">matrix</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;The transitivity is related to the clustering coefficient.&quot;&quot;&quot;</span>
  
  <span class="n">n</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
  <span class="n">t</span> <span class="o">=</span> <span class="n">weighted_triangle_number</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span>
  <span class="n">k</span> <span class="o">=</span> <span class="n">unweighted_node_degree</span><span class="p">(</span><span class="n">matrix</span><span class="p">)</span> <span class="c1"># here we use the max possible weights as reference</span>
  
  <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="mi">2</span> <span class="o">*</span> <span class="n">t</span><span class="p">)</span> <span class="o">/</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">k</span> <span class="o">*</span> <span class="p">(</span><span class="n">k</span> <span class="o">-</span> <span class="mi">1</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Compare-Small-World-coefficient-with-other-graph-measures">Compare Small-World coefficient with other graph measures<a class="anchor-link" href="#Compare-Small-World-coefficient-with-other-graph-measures">&#182;</a></h2><p>Calculate all interesting measures on a set of graphs and check their correlation.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[52]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># first generate multiple graphs to compare</span>
<span class="n">graphs</span> <span class="o">=</span> <span class="p">[</span><span class="n">generate_graph</span><span class="p">(</span><span class="n">n_nodes</span><span class="o">=</span><span class="mi">30</span><span class="p">,</span> <span class="n">regularity</span><span class="o">=</span><span class="mf">0.01</span><span class="o">*</span><span class="n">i</span><span class="p">)</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">100</span><span class="p">)]</span>

<span class="c1"># plot some of them</span>
<span class="n">plot_graph</span><span class="p">(</span><span class="n">graphs</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="s2">&quot;First Graph&quot;</span><span class="p">)</span>
<span class="n">plot_graph</span><span class="p">(</span><span class="n">graphs</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">],</span> <span class="s2">&quot;Last Graph&quot;</span><span class="p">)</span>


<span class="c1"># calculate different graph measures</span>
<span class="n">characteristic_paths</span> <span class="o">=</span>  <span class="p">[</span><span class="n">weighted_characteristic_path_length</span><span class="p">(</span><span class="n">graph</span><span class="p">)</span> <span class="k">for</span> <span class="n">graph</span> <span class="ow">in</span> <span class="n">graphs</span><span class="p">]</span>
<span class="n">global_efficiencies</span> <span class="o">=</span>   <span class="p">[</span><span class="n">weighted_global_efficiency</span><span class="p">(</span><span class="n">graph</span><span class="p">)</span> <span class="k">for</span> <span class="n">graph</span> <span class="ow">in</span> <span class="n">graphs</span><span class="p">]</span>
<span class="n">clustering_coeffs</span> <span class="o">=</span>     <span class="p">[</span><span class="n">weighted_clustering_coeff</span><span class="p">(</span><span class="n">graph</span><span class="p">)</span> <span class="k">for</span> <span class="n">graph</span> <span class="ow">in</span> <span class="n">graphs</span><span class="p">]</span>
<span class="n">transitivities</span> <span class="o">=</span>        <span class="p">[</span><span class="n">weighted_transitivity</span><span class="p">(</span><span class="n">graph</span><span class="p">)</span> <span class="k">for</span> <span class="n">graph</span> <span class="ow">in</span> <span class="n">graphs</span><span class="p">]</span>
<span class="n">sw_sigma</span> <span class="o">=</span>      <span class="p">[</span><span class="n">weighted_sw_sigma</span><span class="p">(</span><span class="n">graph</span><span class="p">,</span> <span class="n">n_avg</span><span class="o">=</span><span class="mi">3</span><span class="p">)</span> <span class="k">for</span> <span class="n">graph</span> <span class="ow">in</span> <span class="n">graphs</span><span class="p">]</span>
<span class="n">sw_omega</span> <span class="o">=</span>      <span class="p">[</span><span class="n">weighted_sw_omega</span><span class="p">(</span><span class="n">graph</span><span class="p">,</span> <span class="n">n_avg</span><span class="o">=</span><span class="mi">3</span><span class="p">)</span> <span class="k">for</span> <span class="n">graph</span> <span class="ow">in</span> <span class="n">graphs</span><span class="p">]</span>
<span class="n">sw_index</span> <span class="o">=</span>      <span class="p">[</span><span class="n">weighted_sw_index</span><span class="p">(</span><span class="n">graph</span><span class="p">,</span> <span class="n">n_avg</span><span class="o">=</span><span class="mi">3</span><span class="p">)</span> <span class="k">for</span> <span class="n">graph</span> <span class="ow">in</span> <span class="n">graphs</span><span class="p">]</span>


<span class="c1"># concatenate them and put them into a correlation matrix</span>
<span class="n">measures</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">vstack</span><span class="p">([</span><span class="n">characteristic_paths</span><span class="p">,</span> <span class="n">global_efficiencies</span><span class="p">,</span>
                      <span class="n">clustering_coeffs</span><span class="p">,</span> <span class="n">transitivities</span><span class="p">,</span>
                      <span class="n">sw_sigma</span><span class="p">,</span> <span class="n">sw_omega</span><span class="p">,</span> <span class="n">sw_index</span><span class="p">])</span>
<span class="n">corr_matrix</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">corrcoef</span><span class="p">(</span><span class="n">measures</span><span class="p">)</span>


<span class="c1"># plot the results</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pcolormesh</span><span class="p">(</span><span class="n">corr_matrix</span><span class="p">,</span> <span class="n">vmin</span><span class="o">=-</span><span class="mi">1</span><span class="p">,</span> <span class="n">vmax</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">cmap</span><span class="o">=</span><span class="s2">&quot;RdBu&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Correlations of all measures&quot;</span><span class="p">)</span>
<span class="n">labels</span> <span class="o">=</span> <span class="p">[</span><span class="s2">&quot;Char. Path&quot;</span><span class="p">,</span> <span class="s2">&quot;Global Eff.&quot;</span><span class="p">,</span> <span class="s2">&quot;Clust. Coef.&quot;</span><span class="p">,</span> <span class="s2">&quot;Trans.&quot;</span><span class="p">,</span> 
          <span class="s2">&quot;SW $\sigma$&quot;</span><span class="p">,</span> <span class="s2">&quot;SW $\omega$&quot;</span><span class="p">,</span> <span class="s2">&quot;SWI&quot;</span><span class="p">]</span>
<span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">gca</span><span class="p">()</span>
<span class="n">ax</span><span class="o">.</span><span class="n">set_xticklabels</span><span class="p">(</span><span class="n">labels</span><span class="p">)</span>
<span class="n">ax</span><span class="o">.</span><span class="n">set_yticklabels</span><span class="p">(</span><span class="n">labels</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xticks</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">labels</span><span class="p">))</span><span class="o">+</span><span class="mf">0.5</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">yticks</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">labels</span><span class="p">))</span><span class="o">+</span><span class="mf">0.5</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">colorbar</span><span class="p">(</span><span class="n">ticks</span><span class="o">=</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="o">-.</span><span class="mi">5</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="o">.</span><span class="mi">5</span><span class="p">,</span> <span class="mi">1</span><span class="p">])</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="c1"># also print the numbers</span>
<span class="nb">print</span><span class="p">(</span><span class="n">corr_matrix</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>[[ 1.         -0.89587379 -0.51657186 -0.51657186  0.51961655 -0.01364881
   0.07509898]
 [-0.89587379  1.          0.13466635  0.13466635 -0.73441356 -0.36105858
  -0.23534892]
 [-0.51657186  0.13466635  1.          1.          0.21641263  0.72794409
   0.23486155]
 [-0.51657186  0.13466635  1.          1.          0.21641263  0.72794409
   0.23486155]
 [ 0.51961655 -0.73441356  0.21641263  0.21641263  1.          0.66541898
   0.36286005]
 [-0.01364881 -0.36105858  0.72794409  0.72794409  0.66541898  1.
   0.44968277]
 [ 0.07509898 -0.23534892  0.23486155  0.23486155  0.36286005  0.44968277
   1.        ]]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Literature:">Literature:<a class="anchor-link" href="#Literature:">&#182;</a></h2><p>Rubinov, M., &amp; Sporns, O. (2010). Complex network measures of brain connectivity: uses and interpretations. Neuroimage, 52(3), 1059-1069.</p>
<p>Saramäki, J., Kivelä, M., Onnela, J. P., Kaski, K., &amp; Kertesz, J. (2007). Generalizations of the clustering coefficient to weighted complex networks. Physical Review E, 75(2), 027105.</p>
<p>Sporns, O., &amp; Zwi, J. D. (2004). The small world of the cerebral cortex. Neuroinformatics, 2(2), 145-162.</p>

</div>
</div>
</div>
    </div>
  </div>
</body>

 


</html>

