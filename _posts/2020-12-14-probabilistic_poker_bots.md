---
title: "Probabilistic Poker Bots"
excerpt: "Define automated Poker playing algorithms and play against them."
header:
  teaser: "/assets/images/posts/poker_wikimedia.jpg"
  overlay_image: "/assets/images/posts/poker_wikimedia.jpg"
  caption: "Photo credit: [**Wikimedia Commons**](https://commons.wikimedia.org/wiki/File:Card_games_and_game_tokens_01.jpg)"
  #actions:
  #  - label: "Learn more"
  #    url: "https://commons.wikimedia.org/wiki/File:Card_games_and_game_tokens_01.jpg"
tags:
  - Probability Theory
  - Statistics
last_modified_at: 2020-12-14T10:22:00-04:00
---


<!---
<style>
iframe{height:20000px !important;}
</style>
<div style="margin-right:-30%;">
  <script src="https://gist.github.com/DiGyt/8fc610f08a8fe677b2d8e59c914a4226.js"></script>
</div>
-->



<!DOCTYPE html>
<html>
<head><meta charset="utf-8" />

<title>Probabilistic_Poker_Bots_I</title>

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
<h1 id="Probabilistic-Poker-Bots">Probabilistic Poker Bots<a class="anchor-link" href="#Probabilistic-Poker-Bots">&#182;</a></h1><hr>
<p>In this notebook I will show you how to play Poker with Python, write automated Poker algorithms and see how they perform against each other and human players.</p>
<p>First of all, we will define a poker game from scratch, using core Python. After creating everything we need for a full-fledged, well-formed game, we will introduce different types of automated playing algorithms and see how they comete against each other. First we will introduce very simple classes who have only basic Poker knowledge, later we will create smarter classes that can estimate their own winning probabilities and use these as a basis for their decisions. Finally, you will be able to play against these automated algorithms and see how they perform against yourself.</p>
<p>This notebook also aims to showcase what you can accomplish with Python, while trying to keep everything as intuitive and comprehensible as possible - even if you're not that familiar with Python.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Basics:-Define-Poker-hands.">Basics: Define Poker hands.<a class="anchor-link" href="#Basics:-Define-Poker-hands.">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>First of all, we have to define the most basic properties we will use: Names and suits of a poker deck, and other game-specific names. We also define a function that creates a new shuffled deck, from which we can then draw single cards.</p>
<p>As you can see, our poker game is purely written in Python core, with only one dependence on the "random" module (which I'm somehow really proud of). However, we will later use matplotlib to visualize our data.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">random</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>

<span class="c1"># define some constant variables that we will need troughout the game</span>
<span class="n">CARD_SUITS</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;clubs&#39;</span><span class="p">,</span> <span class="s1">&#39;diamonds&#39;</span><span class="p">,</span> <span class="s1">&#39;hearts&#39;</span><span class="p">,</span> <span class="s1">&#39;spades&#39;</span><span class="p">]</span>
<span class="n">CARD_RANKS</span> <span class="o">=</span> <span class="p">[</span><span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="mi">7</span><span class="p">,</span> <span class="mi">8</span><span class="p">,</span> <span class="mi">9</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="s1">&#39;J&#39;</span><span class="p">,</span> <span class="s1">&#39;Q&#39;</span><span class="p">,</span> <span class="s1">&#39;K&#39;</span><span class="p">,</span> <span class="s1">&#39;A&#39;</span><span class="p">]</span>
<span class="n">GAME_STATES</span> <span class="o">=</span> <span class="p">[</span><span class="s2">&quot;Pre-Flop&quot;</span><span class="p">,</span> <span class="s2">&quot;Flop&quot;</span><span class="p">,</span> <span class="s2">&quot;River&quot;</span><span class="p">,</span> <span class="s2">&quot;Turn&quot;</span><span class="p">]</span>
<span class="n">CARD_COMBOS</span> <span class="o">=</span> <span class="p">[</span><span class="s2">&quot;High Card&quot;</span><span class="p">,</span> <span class="s2">&quot;Pair&quot;</span><span class="p">,</span> <span class="s2">&quot;Two Pairs&quot;</span><span class="p">,</span> <span class="s2">&quot;Three of a kind&quot;</span><span class="p">,</span>
               <span class="s2">&quot;Straight&quot;</span><span class="p">,</span> <span class="s2">&quot;Flush&quot;</span><span class="p">,</span> <span class="s2">&quot;Full House&quot;</span><span class="p">,</span> <span class="s2">&quot;Four of a Kind&quot;</span><span class="p">,</span>
               <span class="s2">&quot;Straight Flush&quot;</span><span class="p">,</span> <span class="s2">&quot;Royal Flush&quot;</span><span class="p">]</span>

<span class="k">def</span> <span class="nf">new_deck</span><span class="p">():</span>
  <span class="sd">&quot;&quot;&quot;Create a new shuffled deck.&quot;&quot;&quot;</span>
  <span class="n">deck</span> <span class="o">=</span> <span class="p">[]</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">CARD_RANKS</span><span class="p">:</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="n">CARD_SUITS</span><span class="p">:</span>
      <span class="n">deck</span><span class="o">.</span><span class="n">append</span><span class="p">((</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">))</span>
  <span class="n">random</span><span class="o">.</span><span class="n">shuffle</span><span class="p">(</span><span class="n">deck</span><span class="p">)</span>
  <span class="k">return</span> <span class="n">deck</span>

<span class="c1"># create a new deck and draw 7 cards</span>
<span class="n">deck</span> <span class="o">=</span> <span class="n">new_deck</span><span class="p">()</span>
<span class="n">hand</span> <span class="o">=</span> <span class="p">[</span><span class="n">deck</span><span class="o">.</span><span class="n">pop</span><span class="p">()</span> <span class="k">for</span> <span class="n">card</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">7</span><span class="p">)]</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Hand of seven cards: &quot;</span><span class="p">,</span> <span class="n">hand</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Hand of seven cards:  [(&#39;A&#39;, &#39;diamonds&#39;), (7, &#39;spades&#39;), (9, &#39;hearts&#39;), (&#39;K&#39;, &#39;spades&#39;), (7, &#39;diamonds&#39;), (5, &#39;clubs&#39;), (&#39;Q&#39;, &#39;diamonds&#39;)]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>In the output above, you see that cards are defined as tuples of <code>(rank, suit)</code>. A hand is represented as a list of cards. We can draw new cards from the top of our shuffled deck by using <code>card = deck.pop()</code> or we can create a new shuffled deck with <code>deck = new_deck()</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now we need to define functions that recognize whether a given Poker card combination is given in a specific hand.
The functions in the next block are conceptually inspired by <a href="https://codegolf.stackexchange.com/questions/33149/probability-to-win-a-hand-of-poker-texas-hold-em">this stackexchange post</a>. They are slower than my initial solution and take a lot of lines to define, but their structure is clearer and more intuitive. I defined the functions in a way that they return the highest given combination (e.g. the highest pair in a set of cards). If the combination is not present at all, the functions will return <code>None</code>. You will see an example of this below.</p>
<p>You don't need to read through all of the code as the functions should be pretty self-explanatory.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">rank</span><span class="p">(</span><span class="n">card</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Returns the rank of a card.&quot;&quot;&quot;</span>
  <span class="k">return</span> <span class="n">CARD_RANKS</span><span class="o">.</span><span class="n">index</span><span class="p">(</span><span class="n">card</span><span class="p">[</span><span class="mi">0</span><span class="p">])</span>

<span class="k">def</span> <span class="nf">suit</span><span class="p">(</span><span class="n">card</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Returns the suit of a card.&quot;&quot;&quot;</span>
  <span class="k">return</span> <span class="n">card</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span>

<span class="k">def</span> <span class="nf">amounts</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Returns tuples of the rank set sorted by number of their occurence.&quot;&quot;&quot;</span>
  <span class="n">vals</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="n">rank</span><span class="p">,</span> <span class="n">hand</span><span class="p">))</span>
  <span class="k">return</span> <span class="p">[(</span><span class="n">vals</span><span class="o">.</span><span class="n">count</span><span class="p">(</span><span class="n">val</span><span class="p">),</span> <span class="n">val</span><span class="p">)</span> <span class="k">for</span> <span class="n">val</span> <span class="ow">in</span> <span class="nb">set</span><span class="p">(</span><span class="n">vals</span><span class="p">)]</span> <span class="o">+</span> <span class="p">[(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">),</span> <span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">)]</span>

<span class="k">def</span> <span class="nf">high_card</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Returns the rank of the highest card.&quot;&quot;&quot;</span>
  <span class="k">return</span> <span class="nb">max</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="n">rank</span><span class="p">,</span> <span class="n">hand</span><span class="p">)))</span>

<span class="k">def</span> <span class="nf">pair</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Gives the rank of the best pair if there&#39;s a pair. Else returns None.&quot;&quot;&quot;</span>
  <span class="n">sums</span> <span class="o">=</span> <span class="n">amounts</span><span class="p">(</span><span class="n">hand</span><span class="p">)</span>
  <span class="n">found</span> <span class="o">=</span> <span class="p">[</span><span class="n">val</span> <span class="k">for</span> <span class="n">val</span> <span class="ow">in</span> <span class="n">sums</span> <span class="k">if</span> <span class="n">val</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">2</span><span class="p">]</span>
  <span class="k">return</span> <span class="nb">max</span><span class="p">(</span><span class="n">found</span><span class="p">)[</span><span class="mi">1</span><span class="p">]</span> <span class="k">if</span> <span class="n">found</span> <span class="o">!=</span> <span class="p">[]</span> <span class="k">else</span> <span class="kc">None</span>

<span class="k">def</span> <span class="nf">three_of_a_kind</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Gives the rank of the best triple if there&#39;s a triple. Else None.&quot;&quot;&quot;</span>
  <span class="n">sums</span> <span class="o">=</span> <span class="n">amounts</span><span class="p">(</span><span class="n">hand</span><span class="p">)</span>
  <span class="n">found</span> <span class="o">=</span> <span class="p">[</span><span class="n">val</span> <span class="k">for</span> <span class="n">val</span> <span class="ow">in</span> <span class="n">sums</span> <span class="k">if</span> <span class="n">val</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">3</span><span class="p">]</span>
  <span class="k">return</span> <span class="nb">max</span><span class="p">(</span><span class="n">found</span><span class="p">)[</span><span class="mi">1</span><span class="p">]</span> <span class="k">if</span> <span class="n">found</span> <span class="o">!=</span> <span class="p">[]</span> <span class="k">else</span> <span class="kc">None</span>

<span class="k">def</span> <span class="nf">four_of_a_kind</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Gives the rank of the best four-of-a-kind if there&#39;s one. Else None.&quot;&quot;&quot;</span>
  <span class="n">sums</span> <span class="o">=</span> <span class="n">amounts</span><span class="p">(</span><span class="n">hand</span><span class="p">)</span>
  <span class="n">found</span> <span class="o">=</span> <span class="p">[</span><span class="n">val</span> <span class="k">for</span> <span class="n">val</span> <span class="ow">in</span> <span class="n">sums</span> <span class="k">if</span> <span class="n">val</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">4</span><span class="p">]</span>
  <span class="k">return</span> <span class="nb">max</span><span class="p">(</span><span class="n">found</span><span class="p">)[</span><span class="mi">1</span><span class="p">]</span> <span class="k">if</span> <span class="n">found</span> <span class="o">!=</span> <span class="p">[]</span> <span class="k">else</span> <span class="kc">None</span>

<span class="k">def</span> <span class="nf">two_pairs</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Gives the rank of the best pair if there&#39;s two pairs. Else None.&quot;&quot;&quot;</span>
  <span class="n">sorted_cards</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">amounts</span><span class="p">(</span><span class="n">hand</span><span class="p">),</span> <span class="n">reverse</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
  <span class="k">if</span> <span class="n">sorted_cards</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="mi">0</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">2</span> <span class="ow">and</span> <span class="n">sorted_cards</span><span class="p">[</span><span class="mi">1</span><span class="p">][</span><span class="mi">0</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">2</span><span class="p">:</span>
    <span class="k">return</span> <span class="n">sorted_cards</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="mi">1</span><span class="p">]</span>
  <span class="k">else</span><span class="p">:</span>
    <span class="k">return</span> <span class="kc">None</span>

<span class="k">def</span> <span class="nf">full_house</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Gives the rank of the best triple if there&#39;s a full house. Else None.&quot;&quot;&quot;</span>
  <span class="n">sorted_cards</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">amounts</span><span class="p">(</span><span class="n">hand</span><span class="p">),</span> <span class="n">reverse</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
  <span class="k">if</span> <span class="n">sorted_cards</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="mi">0</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">3</span> <span class="ow">and</span> <span class="n">sorted_cards</span><span class="p">[</span><span class="mi">1</span><span class="p">][</span><span class="mi">0</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">2</span><span class="p">:</span>
    <span class="k">return</span> <span class="n">sorted_cards</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="mi">1</span><span class="p">]</span>
  <span class="k">else</span><span class="p">:</span>
    <span class="k">return</span> <span class="kc">None</span>

<span class="k">def</span> <span class="nf">straight</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Gives the highest rank of the straight if there&#39;s a straight. Else None.&quot;&quot;&quot;</span>
  <span class="n">vals</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="nb">sorted</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="n">rank</span><span class="p">,</span> <span class="n">hand</span><span class="p">)))</span>
  <span class="n">straight</span> <span class="o">=</span> <span class="kc">None</span>
  <span class="k">if</span> <span class="nb">all</span><span class="p">(</span><span class="n">c</span> <span class="ow">in</span> <span class="n">vals</span> <span class="k">for</span> <span class="n">c</span> <span class="ow">in</span> <span class="p">(</span><span class="mi">12</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">)):</span> <span class="c1"># straight with (A, 2, 3, 4, 5)</span>
    <span class="n">straight</span> <span class="o">=</span> <span class="mi">3</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">9</span><span class="p">):</span>
    <span class="k">if</span> <span class="nb">all</span><span class="p">(</span><span class="n">c</span> <span class="ow">in</span> <span class="n">vals</span> <span class="k">for</span> <span class="n">c</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">i</span><span class="p">,</span> <span class="n">i</span> <span class="o">+</span> <span class="mi">5</span><span class="p">)):</span>
      <span class="n">straight</span> <span class="o">=</span> <span class="n">i</span> <span class="o">+</span> <span class="mi">4</span>
  <span class="k">return</span> <span class="n">straight</span>

<span class="k">def</span> <span class="nf">flush</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Gives the highest rank of the flush if there&#39;s a flush. Else None.&quot;&quot;&quot;</span>
  <span class="n">suits</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="n">suit</span><span class="p">,</span> <span class="n">hand</span><span class="p">))</span>
  <span class="n">max_suit</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="nb">zip</span><span class="p">([</span><span class="n">suits</span><span class="o">.</span><span class="n">count</span><span class="p">(</span><span class="n">suit</span><span class="p">)</span> <span class="k">for</span> <span class="n">suit</span> <span class="ow">in</span> <span class="n">suits</span><span class="p">],</span> <span class="n">suits</span><span class="p">))[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>
  <span class="k">if</span> <span class="n">max_suit</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">5</span><span class="p">:</span>
    <span class="n">vals</span> <span class="o">=</span> <span class="p">[</span><span class="n">CARD_RANKS</span><span class="o">.</span><span class="n">index</span><span class="p">(</span><span class="n">val</span><span class="p">)</span> <span class="k">for</span> <span class="n">val</span><span class="p">,</span> <span class="n">suit</span> <span class="ow">in</span> <span class="n">hand</span> <span class="k">if</span> <span class="n">suit</span> <span class="o">==</span> <span class="n">max_suit</span><span class="p">[</span><span class="mi">1</span><span class="p">]]</span>
    <span class="k">return</span> <span class="nb">max</span><span class="p">(</span><span class="n">vals</span><span class="p">)</span>
  <span class="k">else</span><span class="p">:</span>
    <span class="k">return</span> <span class="kc">None</span>

<span class="k">def</span> <span class="nf">straight_flush</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Gives the highest rank of a straight flush if there is one. Else None.&quot;&quot;&quot;</span>
  <span class="n">suits</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="n">suit</span><span class="p">,</span> <span class="n">hand</span><span class="p">))</span>
  <span class="n">max_suit</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="nb">zip</span><span class="p">([</span><span class="n">suits</span><span class="o">.</span><span class="n">count</span><span class="p">(</span><span class="n">suit</span><span class="p">)</span> <span class="k">for</span> <span class="n">suit</span> <span class="ow">in</span> <span class="n">suits</span><span class="p">],</span> <span class="n">suits</span><span class="p">))[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>
  <span class="n">straight</span> <span class="o">=</span> <span class="kc">None</span>
  <span class="k">if</span> <span class="n">max_suit</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">5</span><span class="p">:</span>
    <span class="n">vals</span> <span class="o">=</span> <span class="p">[</span><span class="n">CARD_RANKS</span><span class="o">.</span><span class="n">index</span><span class="p">(</span><span class="n">val</span><span class="p">)</span> <span class="k">for</span> <span class="n">val</span><span class="p">,</span> <span class="n">suit</span> <span class="ow">in</span> <span class="n">hand</span> <span class="k">if</span> <span class="n">suit</span> <span class="o">==</span> <span class="n">max_suit</span><span class="p">[</span><span class="mi">1</span><span class="p">]]</span>
    <span class="k">if</span> <span class="nb">all</span><span class="p">(</span><span class="n">c</span> <span class="ow">in</span> <span class="n">vals</span> <span class="k">for</span> <span class="n">c</span> <span class="ow">in</span> <span class="p">(</span><span class="mi">12</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">)):</span>
      <span class="n">straight</span> <span class="o">=</span> <span class="mi">3</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">12</span><span class="p">):</span>
      <span class="k">if</span> <span class="nb">all</span><span class="p">(</span><span class="n">c</span> <span class="ow">in</span> <span class="n">vals</span> <span class="k">for</span> <span class="n">c</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">i</span><span class="p">,</span> <span class="n">i</span> <span class="o">+</span> <span class="mi">5</span><span class="p">)):</span>
        <span class="n">straight</span> <span class="o">=</span> <span class="n">i</span> <span class="o">+</span> <span class="mi">4</span>
  <span class="k">return</span> <span class="n">straight</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>We should also include some handy functions that help us to find the best combination in a given hand, verbalize them and compare between different hands.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">score</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Score a given hand by the best combo and the card driving the combo.&quot;&quot;&quot;</span>
  <span class="n">combos</span> <span class="o">=</span> <span class="p">[</span><span class="n">high_card</span><span class="p">,</span> <span class="n">pair</span><span class="p">,</span> <span class="n">two_pairs</span><span class="p">,</span> <span class="n">three_of_a_kind</span><span class="p">,</span> <span class="n">straight</span><span class="p">,</span> <span class="n">flush</span><span class="p">,</span>
            <span class="n">full_house</span><span class="p">,</span> <span class="n">four_of_a_kind</span><span class="p">,</span> <span class="n">straight_flush</span><span class="p">]</span>
  <span class="k">for</span> <span class="n">index</span><span class="p">,</span> <span class="n">combo_func</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">combos</span><span class="p">):</span>
    <span class="n">result</span> <span class="o">=</span> <span class="n">combo_func</span><span class="p">(</span><span class="n">hand</span><span class="p">)</span>
    <span class="k">if</span> <span class="n">result</span> <span class="o">!=</span> <span class="kc">None</span><span class="p">:</span>
      <span class="n">combo_index</span> <span class="o">=</span> <span class="n">index</span>
      <span class="n">determinant</span> <span class="o">=</span> <span class="n">result</span>
  <span class="c1"># make Straight Flush with Ace a Royal Flush</span>
  <span class="n">combo_index</span> <span class="o">=</span> <span class="mi">9</span> <span class="k">if</span> <span class="p">(</span><span class="n">combo_index</span> <span class="o">==</span> <span class="mi">8</span> <span class="ow">and</span> <span class="n">determinant</span> <span class="o">==</span> <span class="mi">12</span><span class="p">)</span> <span class="k">else</span> <span class="n">combo_index</span>
  <span class="k">return</span> <span class="n">combo_index</span><span class="p">,</span> <span class="n">determinant</span>


<span class="k">def</span> <span class="nf">raw_score</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Raw score of the cards. Relevant when a Kicker decides the game.&quot;&quot;&quot;</span>
  <span class="n">vals</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="n">rank</span><span class="p">,</span> <span class="n">hand</span><span class="p">))</span>
  <span class="k">return</span> <span class="nb">sum</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">CARD_RANKS</span><span class="p">)</span><span class="o">**</span><span class="n">i</span> <span class="o">*</span> <span class="n">v</span> <span class="k">for</span> <span class="n">i</span><span class="p">,</span> <span class="n">v</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">vals</span><span class="p">))</span>


<span class="k">def</span> <span class="nf">name_hand</span><span class="p">(</span><span class="n">hand</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Return a verbal description of the best combo in the given hand.&quot;&quot;&quot;</span>
  <span class="n">index</span><span class="p">,</span> <span class="n">determinant</span> <span class="o">=</span> <span class="n">score</span><span class="p">(</span><span class="n">hand</span><span class="p">)</span>
  <span class="k">return</span> <span class="n">CARD_COMBOS</span><span class="p">[</span><span class="n">index</span><span class="p">]</span> <span class="o">+</span> <span class="s2">&quot; with &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">CARD_RANKS</span><span class="p">[</span><span class="n">determinant</span><span class="p">])</span>


<span class="k">def</span> <span class="nf">compare_hands</span><span class="p">(</span><span class="n">hands</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Evaluate a number of hands and return the indices of the winner(s).&quot;&quot;&quot;</span>
  <span class="n">combos</span><span class="p">,</span> <span class="n">determinants</span> <span class="o">=</span> <span class="nb">zip</span><span class="p">(</span><span class="o">*</span><span class="p">(</span><span class="n">score</span><span class="p">(</span><span class="n">hand</span><span class="p">)</span> <span class="k">for</span> <span class="n">hand</span> <span class="ow">in</span> <span class="n">hands</span><span class="p">))</span>
  <span class="n">raw_scores</span> <span class="o">=</span> <span class="p">[</span><span class="n">raw_score</span><span class="p">(</span><span class="n">hand</span><span class="p">)</span> <span class="k">for</span> <span class="n">hand</span> <span class="ow">in</span> <span class="n">hands</span><span class="p">]</span>
  <span class="n">ranks</span> <span class="o">=</span> <span class="nb">zip</span><span class="p">(</span><span class="n">combos</span><span class="p">,</span> <span class="n">determinants</span><span class="p">,</span> <span class="n">raw_scores</span><span class="p">,</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">combos</span><span class="p">)))</span>
  <span class="n">ranks</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">ranks</span><span class="p">,</span> <span class="n">reverse</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
  <span class="n">winners</span> <span class="o">=</span> <span class="p">[</span><span class="n">idx</span> <span class="k">for</span> <span class="n">combo</span><span class="p">,</span> <span class="n">det</span><span class="p">,</span> <span class="n">rsc</span><span class="p">,</span> <span class="n">idx</span> <span class="ow">in</span> <span class="n">ranks</span> <span class="k">if</span> <span class="p">(</span><span class="n">combo</span><span class="p">,</span> <span class="n">det</span><span class="p">,</span> <span class="n">rsc</span><span class="p">)</span> <span class="o">==</span> <span class="n">ranks</span><span class="p">[</span><span class="mi">0</span><span class="p">][:</span><span class="mi">3</span><span class="p">]]</span>
  <span class="k">return</span> <span class="n">winners</span>


<span class="k">def</span> <span class="nf">name_rank</span><span class="p">(</span><span class="n">rank</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Gives the card rank name instead of the numerical rank.&quot;&quot;&quot;</span>
  <span class="k">return</span> <span class="n">CARD_RANKS</span><span class="p">[</span><span class="n">rank</span><span class="p">]</span> <span class="k">if</span> <span class="n">rank</span> <span class="o">!=</span> <span class="kc">None</span> <span class="k">else</span> <span class="kc">None</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now we can look at a specific hand, e.g. <code>[(4, 'clubs'), (8, 'hearts'), (10, 'spades'), (9, 'diamonds'), ('J', 'spades'), ('Q', 'spades'), ('Q', 'hearts')]</code> and check it for specific combinations. We can for example look if there is a pair or a straight in our hand, our simply print out the best combination in our hand.</p>
<p>In contrast to most of the Poker evaluation functions I found on the web, these functions are not restricted to a specific hand size, but work correctly with any given card number, which especially helps us when not all game are known yet.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">hand</span> <span class="o">=</span> <span class="p">[(</span><span class="mi">4</span><span class="p">,</span> <span class="s1">&#39;clubs&#39;</span><span class="p">),</span> <span class="p">(</span><span class="mi">8</span><span class="p">,</span> <span class="s1">&#39;hearts&#39;</span><span class="p">),</span> <span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="s1">&#39;spades&#39;</span><span class="p">),</span> <span class="p">(</span><span class="mi">9</span><span class="p">,</span> <span class="s1">&#39;diamonds&#39;</span><span class="p">),</span>
        <span class="p">(</span><span class="s1">&#39;J&#39;</span><span class="p">,</span> <span class="s1">&#39;spades&#39;</span><span class="p">),</span> <span class="p">(</span><span class="s1">&#39;Q&#39;</span><span class="p">,</span> <span class="s1">&#39;spades&#39;</span><span class="p">),</span> <span class="p">(</span><span class="s1">&#39;Q&#39;</span><span class="p">,</span> <span class="s1">&#39;hearts&#39;</span><span class="p">)]</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;First Hand: &quot;</span><span class="p">,</span> <span class="n">hand</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Pair in Hand: &quot;</span><span class="p">,</span> <span class="n">name_rank</span><span class="p">(</span><span class="n">pair</span><span class="p">(</span><span class="n">hand</span><span class="p">)))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Straight in Hand: &quot;</span><span class="p">,</span> <span class="n">name_rank</span><span class="p">(</span><span class="n">straight</span><span class="p">(</span><span class="n">hand</span><span class="p">)))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best Combo in hand: &quot;</span><span class="p">,</span> <span class="n">name_hand</span><span class="p">(</span><span class="n">hand</span><span class="p">))</span>

<span class="n">second_hand</span> <span class="o">=</span> <span class="p">[(</span><span class="mi">4</span><span class="p">,</span> <span class="s1">&#39;diamonds&#39;</span><span class="p">),</span> <span class="p">(</span><span class="mi">5</span><span class="p">,</span> <span class="s1">&#39;diamonds&#39;</span><span class="p">)]</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">Second Hand: &quot;</span><span class="p">,</span> <span class="n">second_hand</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Triple in Hand: &quot;</span><span class="p">,</span> <span class="n">name_rank</span><span class="p">(</span><span class="n">three_of_a_kind</span><span class="p">(</span><span class="n">second_hand</span><span class="p">)))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;High Card in Hand: &quot;</span><span class="p">,</span> <span class="n">name_rank</span><span class="p">(</span><span class="n">high_card</span><span class="p">(</span><span class="n">second_hand</span><span class="p">)))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best Combo in hand: &quot;</span><span class="p">,</span> <span class="n">name_hand</span><span class="p">(</span><span class="n">second_hand</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>First Hand:  [(4, &#39;clubs&#39;), (8, &#39;hearts&#39;), (10, &#39;spades&#39;), (9, &#39;diamonds&#39;), (&#39;J&#39;, &#39;spades&#39;), (&#39;Q&#39;, &#39;spades&#39;), (&#39;Q&#39;, &#39;hearts&#39;)]
Pair in Hand:  Q
Straight in Hand:  Q
Best Combo in hand:  Straight with Q

Second Hand:  [(4, &#39;diamonds&#39;), (5, &#39;diamonds&#39;)]
Triple in Hand:  None
High Card in Hand:  5
Best Combo in hand:  High Card with 5
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Define-Player-and-Game-classes">Define Player and Game classes<a class="anchor-link" href="#Define-Player-and-Game-classes">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now it's time to build our game. For this, we will define a Player class which is mainly concerned with player and attributes (like what cards or how much money they have) and player actions (e.g. if they want to bet or fold in a given game). These classes again take up some lines, however most actions should be clearly understandable. If not, they might become clear after playing around with them.</p>
<p>Our Game class also has a "verbose" option when defining it. If we initialize a game with <code>Game(players, verbose=True)</code> all actions of game and players will be printed allowing us to track (and later play) the game. However, we can also set <code>verbose=False</code>, in order to omit printing. This will speed up simulations if we want to run a large number of games.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">class</span> <span class="nc">Player</span><span class="p">():</span>

  <span class="k">def</span> <span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">name</span><span class="p">,</span> <span class="n">stock</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Initialize a player object that can play several games.&quot;&quot;&quot;</span>

    <span class="c1"># steady attributes are the player&#39;s name and their money account</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">name</span> <span class="o">=</span> <span class="n">name</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">stock</span> <span class="o">=</span> <span class="n">stock</span>

    <span class="c1"># temporary attributes are player cards, stakes in this game and fold status</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">cards</span> <span class="o">=</span> <span class="p">[</span><span class="kc">None</span><span class="p">,</span> <span class="kc">None</span><span class="p">]</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">folded</span> <span class="o">=</span> <span class="kc">False</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">stakes</span> <span class="o">=</span> <span class="mi">0</span>

  <span class="k">def</span> <span class="fm">__repr__</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Represent a player when the object is called.&quot;&quot;&quot;</span>
    <span class="k">return</span> <span class="s2">&quot;</span><span class="si">{0}</span><span class="s2"> (Player) - stock: </span><span class="si">{1}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">name</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">stock</span><span class="p">)</span>

  <span class="k">def</span> <span class="nf">reset_game</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Reset temporary player attributes.&quot;&quot;&quot;</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">cards</span> <span class="o">=</span> <span class="p">[</span><span class="kc">None</span><span class="p">,</span> <span class="kc">None</span><span class="p">]</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">folded</span> <span class="o">=</span> <span class="kc">False</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">stakes</span> <span class="o">=</span> <span class="mi">0</span>

  <span class="k">def</span> <span class="nf">bet</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">game</span><span class="p">,</span> <span class="n">amount</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Bet an amount in the game.&quot;&quot;&quot;</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">stock</span> <span class="o">-=</span> <span class="n">amount</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">stakes</span> <span class="o">+=</span> <span class="n">amount</span>
    <span class="n">game</span><span class="o">.</span><span class="n">pot</span> <span class="o">+=</span> <span class="n">amount</span>
    <span class="k">if</span> <span class="n">game</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
      <span class="n">msg</span> <span class="o">=</span> <span class="s2">&quot;</span><span class="si">{0}</span><span class="s2"> added </span><span class="si">{1}</span><span class="s2"> to the pot. Player money=</span><span class="si">{2}</span><span class="s2">; Pot money=</span><span class="si">{3}</span><span class="s2">&quot;</span>
      <span class="nb">print</span><span class="p">(</span><span class="n">msg</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">name</span><span class="p">,</span> <span class="n">amount</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">stock</span><span class="p">,</span> <span class="n">game</span><span class="o">.</span><span class="n">pot</span><span class="p">))</span>

  <span class="k">def</span> <span class="nf">call</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">game</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Call to the current max bet.&quot;&quot;&quot;</span>
    <span class="n">max_stakes</span> <span class="o">=</span> <span class="nb">max</span><span class="p">([</span><span class="n">player</span><span class="o">.</span><span class="n">stakes</span> <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">game</span><span class="o">.</span><span class="n">players</span><span class="p">])</span>
    <span class="n">call_diff</span> <span class="o">=</span> <span class="n">max_stakes</span> <span class="o">-</span> <span class="bp">self</span><span class="o">.</span><span class="n">stakes</span>
    <span class="k">if</span> <span class="n">game</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
      <span class="nb">print</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">name</span> <span class="o">+</span> <span class="s2">&quot; called.&quot;</span><span class="p">)</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">bet</span><span class="p">(</span><span class="n">game</span><span class="p">,</span> <span class="n">call_diff</span><span class="p">)</span>

  <span class="k">def</span> <span class="nf">raise_bet</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">game</span><span class="p">,</span> <span class="n">amount</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Raises a bet for a certain amount&quot;&quot;&quot;</span>
    <span class="n">max_stakes</span> <span class="o">=</span> <span class="nb">max</span><span class="p">([</span><span class="n">player</span><span class="o">.</span><span class="n">stakes</span> <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">game</span><span class="o">.</span><span class="n">players</span><span class="p">])</span>
    <span class="n">call_diff</span> <span class="o">=</span> <span class="n">max_stakes</span> <span class="o">-</span> <span class="bp">self</span><span class="o">.</span><span class="n">stakes</span>
    <span class="k">if</span> <span class="n">game</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
      <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="si">{0}</span><span class="s2"> raised the bet by </span><span class="si">{1}</span><span class="s2">.&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">name</span><span class="p">,</span> <span class="n">amount</span><span class="p">))</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">bet</span><span class="p">(</span><span class="n">game</span><span class="p">,</span> <span class="n">call_diff</span> <span class="o">+</span> <span class="n">amount</span><span class="p">)</span>

  <span class="k">def</span> <span class="nf">check</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">game</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Check at the beginning of a betting round.&quot;&quot;&quot;</span>
    <span class="k">if</span> <span class="n">game</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
      <span class="nb">print</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">name</span> <span class="o">+</span> <span class="s2">&quot; checked.&quot;</span><span class="p">)</span>

  <span class="k">def</span> <span class="nf">fold</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">game</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Fold from the game.&quot;&quot;&quot;</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">folded</span> <span class="o">=</span> <span class="kc">True</span>
    <span class="k">if</span> <span class="n">game</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
      <span class="nb">print</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">name</span> <span class="o">+</span> <span class="s2">&quot; folded.&quot;</span><span class="p">)</span>


<span class="k">class</span> <span class="nc">PokerGame</span><span class="p">():</span>

  <span class="k">def</span> <span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">players</span><span class="p">,</span> <span class="n">small_blind</span><span class="o">=</span><span class="mf">1.</span><span class="p">,</span> <span class="n">big_blind</span><span class="o">=</span><span class="mf">2.</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="kc">True</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Initialize a new poker game.&quot;&quot;&quot;</span>

    <span class="k">if</span> <span class="nb">len</span><span class="p">(</span><span class="n">players</span><span class="p">)</span> <span class="o">&gt;</span> <span class="mi">23</span><span class="p">:</span>
      <span class="k">raise</span> <span class="ne">ValueError</span><span class="p">(</span><span class="s2">&quot;Not more than 23 Players can participate in a game.&quot;</span><span class="p">)</span>

    <span class="c1"># initialize all game attributes</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">deck</span> <span class="o">=</span> <span class="n">new_deck</span><span class="p">()</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">public_cards</span> <span class="o">=</span> <span class="p">[(</span><span class="kc">None</span><span class="p">,</span> <span class="kc">None</span><span class="p">)]</span> <span class="o">*</span> <span class="mi">5</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">players</span> <span class="o">=</span> <span class="n">players</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">pot</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">current_state</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">verbose</span> <span class="o">=</span> <span class="n">verbose</span>

    <span class="k">if</span> <span class="bp">self</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
      <span class="n">msg</span> <span class="o">=</span> <span class="s2">&quot;</span><span class="se">\n</span><span class="s2">Game starts. Small blind: </span><span class="si">{0}</span><span class="s2">; Big blind: </span><span class="si">{1}</span><span class="s2">&quot;</span>
      <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">&quot;</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">state</span><span class="p">())</span>
      <span class="nb">print</span><span class="p">(</span><span class="n">msg</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">players</span><span class="p">[</span><span class="o">-</span><span class="mi">2</span><span class="p">]</span><span class="o">.</span><span class="n">name</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">players</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">name</span><span class="p">))</span>

    <span class="c1"># hand out the cards to the players</span>
    <span class="k">for</span> <span class="n">player_idx</span><span class="p">,</span> <span class="n">player</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">players</span><span class="p">):</span>

      <span class="c1"># all players are (back) in the game</span>
      <span class="n">player</span><span class="o">.</span><span class="n">reset_game</span><span class="p">()</span>

      <span class="c1"># every player gets the new top cards of the deck</span>
      <span class="k">for</span> <span class="n">card_idx</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">2</span><span class="p">):</span>
        <span class="n">player</span><span class="o">.</span><span class="n">cards</span><span class="p">[</span><span class="n">card_idx</span><span class="p">]</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">deck</span><span class="o">.</span><span class="n">pop</span><span class="p">()</span>

      <span class="c1"># the latest two positions are big and small blind</span>
      <span class="k">if</span> <span class="n">player_idx</span> <span class="o">==</span> <span class="nb">len</span><span class="p">(</span><span class="n">players</span><span class="p">)</span><span class="o">-</span><span class="mi">2</span><span class="p">:</span>
        <span class="n">player</span><span class="o">.</span><span class="n">bet</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">small_blind</span><span class="p">)</span>
      <span class="k">elif</span> <span class="n">player_idx</span> <span class="o">==</span> <span class="nb">len</span><span class="p">(</span><span class="n">players</span><span class="p">)</span> <span class="o">-</span> <span class="mi">1</span><span class="p">:</span>
        <span class="n">player</span><span class="o">.</span><span class="n">bet</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">big_blind</span><span class="p">)</span>

  <span class="k">def</span> <span class="nf">flop</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Deal out the flop.&quot;&quot;&quot;</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">current_state</span> <span class="o">=</span> <span class="mi">1</span>
    <span class="k">for</span> <span class="n">card_idx</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">3</span><span class="p">):</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">public_cards</span><span class="p">[</span><span class="n">card_idx</span><span class="p">]</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">deck</span><span class="o">.</span><span class="n">pop</span><span class="p">()</span>
    <span class="k">if</span> <span class="bp">self</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
      <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">&quot;</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">state</span><span class="p">())</span>
      <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Open cards after flop: </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">open_cards</span><span class="p">()))</span>

  <span class="k">def</span> <span class="nf">river</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Deal out the river.&quot;&quot;&quot;</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">current_state</span> <span class="o">=</span> <span class="mi">2</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">public_cards</span><span class="p">[</span><span class="mi">3</span><span class="p">]</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">deck</span><span class="o">.</span><span class="n">pop</span><span class="p">()</span>
    <span class="k">if</span> <span class="bp">self</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
      <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">&quot;</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">state</span><span class="p">())</span>
      <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Open cards after river: </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">open_cards</span><span class="p">()))</span>

  <span class="k">def</span> <span class="nf">turn</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Deal out the turn.&quot;&quot;&quot;</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">current_state</span> <span class="o">=</span> <span class="mi">3</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">public_cards</span><span class="p">[</span><span class="mi">4</span><span class="p">]</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">deck</span><span class="o">.</span><span class="n">pop</span><span class="p">()</span>
    <span class="k">if</span> <span class="bp">self</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
      <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">&quot;</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">state</span><span class="p">())</span>
      <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Open cards after turn: </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">open_cards</span><span class="p">()))</span>

  <span class="k">def</span> <span class="nf">showdown</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Compare the hands of all remaning players and return the winner(s).&quot;&quot;&quot;</span>
    <span class="n">remainers</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">players_in</span><span class="p">()</span>
    <span class="n">hands</span> <span class="o">=</span> <span class="p">[</span><span class="n">player</span><span class="o">.</span><span class="n">cards</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">open_cards</span><span class="p">()</span> <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">remainers</span><span class="p">]</span>
    <span class="n">win_indices</span> <span class="o">=</span> <span class="n">compare_hands</span><span class="p">(</span><span class="n">hands</span><span class="p">)</span>
    <span class="n">winners</span> <span class="o">=</span> <span class="p">[</span><span class="n">remainers</span><span class="p">[</span><span class="n">win_idx</span><span class="p">]</span> <span class="k">for</span> <span class="n">win_idx</span> <span class="ow">in</span> <span class="n">win_indices</span><span class="p">]</span>
    <span class="k">if</span> <span class="bp">self</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
      <span class="n">msg</span> <span class="o">=</span> <span class="s2">&quot;Best cards: </span><span class="si">{0}</span><span class="s2"> (</span><span class="si">{1}</span><span class="s2">)</span><span class="se">\n</span><span class="s2">&quot;</span>
      <span class="n">winner_names</span> <span class="o">=</span> <span class="p">[</span><span class="n">winner</span><span class="o">.</span><span class="n">name</span> <span class="k">for</span> <span class="n">winner</span> <span class="ow">in</span> <span class="n">winners</span><span class="p">]</span>
      <span class="n">winning_hand</span> <span class="o">=</span> <span class="n">name_hand</span><span class="p">(</span><span class="n">winners</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">cards</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">open_cards</span><span class="p">())</span>
      <span class="nb">print</span><span class="p">(</span><span class="n">msg</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">winner_names</span><span class="p">,</span> <span class="n">winning_hand</span><span class="p">))</span>
    <span class="k">return</span> <span class="n">winners</span>

  <span class="k">def</span> <span class="nf">payout</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">winners</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Payout the winner(s) and reset the pot money.&quot;&quot;&quot;</span>
    <span class="k">if</span> <span class="nb">len</span><span class="p">(</span><span class="n">winners</span><span class="p">)</span> <span class="o">==</span> <span class="mi">1</span><span class="p">:</span>  <span class="c1"># if there&#39;s only one winner</span>
      <span class="n">winner</span> <span class="o">=</span> <span class="n">winners</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
      <span class="n">winner</span><span class="o">.</span><span class="n">stock</span> <span class="o">+=</span> <span class="bp">self</span><span class="o">.</span><span class="n">pot</span>
      <span class="k">if</span> <span class="bp">self</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
        <span class="n">msg</span> <span class="o">=</span> <span class="s2">&quot;</span><span class="si">{0}</span><span class="s2"> took the pot of </span><span class="si">{1}</span><span class="s2"> and has now </span><span class="si">{2}</span><span class="s2"> in stock.&quot;</span>
        <span class="nb">print</span><span class="p">(</span><span class="n">msg</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">winner</span><span class="o">.</span><span class="n">name</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">pot</span><span class="p">,</span> <span class="n">winner</span><span class="o">.</span><span class="n">stock</span><span class="p">))</span>
    <span class="k">else</span><span class="p">:</span>  <span class="c1"># if there are multiple winners</span>
      <span class="k">for</span> <span class="n">winner</span> <span class="ow">in</span> <span class="n">winners</span><span class="p">:</span>
        <span class="n">share</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">pot</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">winners</span><span class="p">)</span>
        <span class="n">winner</span><span class="o">.</span><span class="n">stock</span> <span class="o">+=</span> <span class="n">share</span>
        <span class="k">if</span> <span class="bp">self</span><span class="o">.</span><span class="n">verbose</span><span class="p">:</span>
          <span class="n">msg</span> <span class="o">=</span> <span class="s2">&quot;</span><span class="si">{0}</span><span class="s2"> took a share of </span><span class="si">{1}</span><span class="s2"> from the pot and has now </span><span class="si">{2}</span><span class="s2"> in stock.&quot;</span>
          <span class="nb">print</span><span class="p">(</span><span class="n">msg</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">winner</span><span class="o">.</span><span class="n">name</span><span class="p">,</span> <span class="n">share</span><span class="p">,</span> <span class="n">winner</span><span class="o">.</span><span class="n">stock</span><span class="p">))</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">pot</span> <span class="o">=</span> <span class="mi">0</span>

  <span class="k">def</span> <span class="nf">open_cards</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Return all the open cards&quot;&quot;&quot;</span>
    <span class="k">return</span> <span class="p">[</span><span class="n">card</span> <span class="k">for</span> <span class="n">card</span> <span class="ow">in</span> <span class="bp">self</span><span class="o">.</span><span class="n">public_cards</span> <span class="k">if</span> <span class="n">card</span> <span class="o">!=</span> <span class="p">(</span><span class="kc">None</span><span class="p">,</span> <span class="kc">None</span><span class="p">)]</span>

  <span class="k">def</span> <span class="nf">state</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Return a string description of the game state.&quot;&quot;&quot;</span>
    <span class="k">return</span> <span class="n">GAME_STATES</span><span class="p">[</span><span class="bp">self</span><span class="o">.</span><span class="n">current_state</span><span class="p">]</span>

  <span class="k">def</span> <span class="nf">print_cards</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Print all the cards in the current game (including from all players).&quot;&quot;&quot;</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">Public cards: &quot;</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">open_cards</span><span class="p">())</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Player cards: &quot;</span><span class="p">)</span>
    <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="bp">self</span><span class="o">.</span><span class="n">players</span><span class="p">:</span>
      <span class="n">msg</span> <span class="o">=</span> <span class="s2">&quot;</span><span class="se">\t</span><span class="si">{0}</span><span class="s2">: </span><span class="si">{1}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">player</span><span class="o">.</span><span class="n">name</span><span class="p">,</span> <span class="n">player</span><span class="o">.</span><span class="n">cards</span><span class="p">)</span>
      <span class="n">msg</span> <span class="o">=</span> <span class="n">msg</span> <span class="o">+</span> <span class="s2">&quot; (Folded)&quot;</span> <span class="k">if</span> <span class="n">player</span><span class="o">.</span><span class="n">folded</span> <span class="k">else</span> <span class="n">msg</span>
      <span class="nb">print</span><span class="p">(</span><span class="n">msg</span><span class="p">)</span>

  <span class="k">def</span> <span class="nf">players_in</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Get a list of the players that are still in the game.&quot;&quot;&quot;</span>
    <span class="k">return</span> <span class="p">[</span><span class="n">player</span> <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="bp">self</span><span class="o">.</span><span class="n">players</span> <span class="k">if</span> <span class="ow">not</span> <span class="n">player</span><span class="o">.</span><span class="n">folded</span><span class="p">]</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Finally! we got our first poker game! Let's start with defining 3 players: Audrey, Janet and Joe. Then we start a new poker game and look at what cards they have.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">audrey</span> <span class="o">=</span> <span class="n">Player</span><span class="p">(</span><span class="s2">&quot;Audrey&quot;</span><span class="p">,</span> <span class="mi">10</span><span class="p">)</span>
<span class="n">janet</span> <span class="o">=</span> <span class="n">Player</span><span class="p">(</span><span class="s2">&quot;Janet&quot;</span><span class="p">,</span> <span class="mi">15</span><span class="p">)</span>
<span class="n">joe</span> <span class="o">=</span> <span class="n">Player</span><span class="p">(</span><span class="s2">&quot;Joe&quot;</span><span class="p">,</span> <span class="mi">12</span><span class="p">)</span>

<span class="c1"># initialize a game and show the cards</span>
<span class="n">game</span> <span class="o">=</span> <span class="n">PokerGame</span><span class="p">([</span><span class="n">audrey</span><span class="p">,</span> <span class="n">janet</span><span class="p">,</span> <span class="n">joe</span><span class="p">],</span> <span class="n">small_blind</span><span class="o">=</span><span class="mf">0.1</span><span class="p">,</span> <span class="n">big_blind</span><span class="o">=</span><span class="mf">0.2</span><span class="p">)</span>
<span class="n">game</span><span class="o">.</span><span class="n">print_cards</span><span class="p">()</span>
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
Pre-Flop

Game starts. Small blind: Janet; Big blind: Joe
Janet added 0.1 to the pot. Player money=14.9; Pot money=0.1
Joe added 0.2 to the pot. Player money=11.8; Pot money=0.30000000000000004

Public cards:  []
Player cards: 
	Audrey: [(&#39;Q&#39;, &#39;spades&#39;), (9, &#39;clubs&#39;)]
	Janet: [(10, &#39;clubs&#39;), (5, &#39;diamonds&#39;)]
	Joe: [(8, &#39;clubs&#39;), (2, &#39;clubs&#39;)]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>We see that there are no public cards (as the flop hasn't been turned yet). Let's let our players place their bets and then turn it. We can also perform a "showdown" at each point during the game to see which player would have won (but without messing up the game).</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># let the players bet</span>
<span class="n">audrey</span><span class="o">.</span><span class="n">check</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>
<span class="n">janet</span><span class="o">.</span><span class="n">raise_bet</span><span class="p">(</span><span class="n">game</span><span class="p">,</span> <span class="mf">1.</span><span class="p">)</span>
<span class="n">joe</span><span class="o">.</span><span class="n">call</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>
<span class="n">audrey</span><span class="o">.</span><span class="n">fold</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>

<span class="c1"># show the flow</span>
<span class="n">game</span><span class="o">.</span><span class="n">flop</span><span class="p">()</span>
<span class="n">game</span><span class="o">.</span><span class="n">print_cards</span><span class="p">()</span>
<span class="n">game</span><span class="o">.</span><span class="n">showdown</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Audrey checked.
Janet raised the bet by 1.0.
Janet added 1.1 to the pot. Player money=13.8; Pot money=1.4000000000000001
Joe called.
Joe added 1.0000000000000002 to the pot. Player money=10.8; Pot money=2.4000000000000004
Audrey folded.

Flop
Open cards after flop: [(4, &#39;clubs&#39;), (&#39;K&#39;, &#39;clubs&#39;), (7, &#39;diamonds&#39;)]

Public cards:  [(4, &#39;clubs&#39;), (&#39;K&#39;, &#39;clubs&#39;), (7, &#39;diamonds&#39;)]
Player cards: 
	Audrey: [(&#39;Q&#39;, &#39;spades&#39;), (9, &#39;clubs&#39;)] (Folded)
	Janet: [(10, &#39;clubs&#39;), (5, &#39;diamonds&#39;)]
	Joe: [(8, &#39;clubs&#39;), (2, &#39;clubs&#39;)]
Best cards: [&#39;Janet&#39;] (High Card with K)

</pre>
</div>
</div>

<div class="output_area">

    <div class="prompt output_prompt">Out[7]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>[Janet (Player) - stock: 13.8]</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># play the river</span>
<span class="n">game</span><span class="o">.</span><span class="n">river</span><span class="p">()</span>

<span class="c1"># play the turn</span>
<span class="n">game</span><span class="o">.</span><span class="n">turn</span><span class="p">()</span>
<span class="n">game</span><span class="o">.</span><span class="n">print_cards</span><span class="p">()</span>
<span class="n">winner</span> <span class="o">=</span> <span class="n">game</span><span class="o">.</span><span class="n">showdown</span><span class="p">()</span>
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
River
Open cards after river: [(4, &#39;clubs&#39;), (&#39;K&#39;, &#39;clubs&#39;), (7, &#39;diamonds&#39;), (7, &#39;clubs&#39;)]

Turn
Open cards after turn: [(4, &#39;clubs&#39;), (&#39;K&#39;, &#39;clubs&#39;), (7, &#39;diamonds&#39;), (7, &#39;clubs&#39;), (4, &#39;diamonds&#39;)]

Public cards:  [(4, &#39;clubs&#39;), (&#39;K&#39;, &#39;clubs&#39;), (7, &#39;diamonds&#39;), (7, &#39;clubs&#39;), (4, &#39;diamonds&#39;)]
Player cards: 
	Audrey: [(&#39;Q&#39;, &#39;spades&#39;), (9, &#39;clubs&#39;)] (Folded)
	Janet: [(10, &#39;clubs&#39;), (5, &#39;diamonds&#39;)]
	Joe: [(8, &#39;clubs&#39;), (2, &#39;clubs&#39;)]
Best cards: [&#39;Joe&#39;] (Flush with K)

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Like this, we can already "hard code" an actual game. However there are no restrictions that force the game to be "well-formed". For example, we can omit bets by players, bet in an unorderly fashion, or even re-draw the cards of our game stages (e.g. if we call <code>game.river()</code> twice, the first river card will just be replaced by a new drawn card and the game will continue as is).</p>
<p>So what we need is to define some framework (possibly a function) that runs through a poker game in an ordere fashion, as defined by the game rules.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">run_game</span><span class="p">(</span><span class="n">players</span><span class="p">,</span> <span class="n">small_blind</span><span class="o">=</span><span class="mf">0.1</span><span class="p">,</span> <span class="n">big_blind</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="kc">True</span><span class="p">):</span>

  <span class="c1"># initialize a new game</span>
  <span class="n">game</span> <span class="o">=</span> <span class="n">PokerGame</span><span class="p">(</span><span class="n">players</span><span class="p">,</span> <span class="n">small_blind</span><span class="p">,</span> <span class="n">big_blind</span><span class="p">,</span> <span class="n">verbose</span><span class="p">)</span>

  <span class="c1"># iterate through all the betting rounds</span>
  <span class="k">for</span> <span class="n">game_state</span> <span class="ow">in</span> <span class="p">[</span><span class="s2">&quot;pre_flop&quot;</span><span class="p">,</span> <span class="n">game</span><span class="o">.</span><span class="n">flop</span><span class="p">,</span> <span class="n">game</span><span class="o">.</span><span class="n">river</span><span class="p">,</span> <span class="n">game</span><span class="o">.</span><span class="n">turn</span><span class="p">]:</span>

    <span class="c1"># turn new cards if the game state requires it</span>
    <span class="k">if</span> <span class="n">callable</span><span class="p">(</span><span class="n">game_state</span><span class="p">):</span>
      <span class="n">game_state</span><span class="p">()</span>

    <span class="c1"># initialize variables for the betting round</span>
    <span class="n">everyone_played</span> <span class="o">=</span> <span class="kc">False</span>
    <span class="n">players_in</span> <span class="o">=</span> <span class="n">game</span><span class="o">.</span><span class="n">players_in</span><span class="p">()</span>
    <span class="n">max_stakes</span> <span class="o">=</span> <span class="nb">max</span><span class="p">([</span><span class="n">player</span><span class="o">.</span><span class="n">stakes</span> <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">game</span><span class="o">.</span><span class="n">players</span><span class="p">])</span>
    <span class="n">cur_idx</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="n">cur_player</span> <span class="o">=</span> <span class="n">players_in</span><span class="p">[</span><span class="n">cur_idx</span><span class="p">]</span>

    <span class="c1"># betting round</span>
    <span class="k">while</span> <span class="n">cur_player</span><span class="o">.</span><span class="n">stakes</span> <span class="o">&lt;</span> <span class="n">max_stakes</span> <span class="ow">or</span> <span class="ow">not</span> <span class="n">everyone_played</span><span class="p">:</span>

      <span class="c1"># current player plays strategy</span>
      <span class="n">cur_player</span><span class="o">.</span><span class="n">strategy</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>  <span class="c1"># Note this line: I&#39;ll explain it just below</span>

      <span class="c1"># break if only one player left</span>
      <span class="k">if</span> <span class="nb">len</span><span class="p">(</span><span class="n">game</span><span class="o">.</span><span class="n">players_in</span><span class="p">())</span> <span class="o">==</span> <span class="mi">1</span><span class="p">:</span>
        <span class="k">break</span>

      <span class="c1"># actualize the new max stakes</span>
      <span class="n">max_stakes</span> <span class="o">=</span> <span class="nb">max</span><span class="p">([</span><span class="n">player</span><span class="o">.</span><span class="n">stakes</span> <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">game</span><span class="o">.</span><span class="n">players</span><span class="p">])</span>

      <span class="c1"># actualize the index for the next player, reset after one iteration</span>
      <span class="n">max_idx_reached</span> <span class="o">=</span> <span class="p">(</span><span class="n">cur_idx</span> <span class="o">&gt;=</span> <span class="nb">len</span><span class="p">(</span><span class="n">players_in</span><span class="p">)</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span>
      <span class="k">if</span> <span class="n">max_idx_reached</span><span class="p">:</span>
        <span class="n">cur_idx</span> <span class="o">=</span> <span class="mi">0</span>
        <span class="n">everyone_played</span> <span class="o">=</span> <span class="kc">True</span>
        <span class="n">players_in</span> <span class="o">=</span> <span class="n">game</span><span class="o">.</span><span class="n">players_in</span><span class="p">()</span>
      <span class="k">else</span><span class="p">:</span>
        <span class="n">cur_idx</span> <span class="o">+=</span> <span class="mi">1</span>

      <span class="c1"># assign the next player to go</span>
      <span class="n">cur_player</span> <span class="o">=</span> <span class="n">players_in</span><span class="p">[</span><span class="n">cur_idx</span><span class="p">]</span>

    <span class="c1"># break if only one player left</span>
    <span class="k">if</span> <span class="nb">len</span><span class="p">(</span><span class="n">game</span><span class="o">.</span><span class="n">players_in</span><span class="p">())</span> <span class="o">==</span> <span class="mi">1</span><span class="p">:</span>
      <span class="k">break</span>
  
  <span class="c1"># decide the winner(s) and pay out the pot</span>
  <span class="n">winners</span> <span class="o">=</span> <span class="n">game</span><span class="o">.</span><span class="n">showdown</span><span class="p">()</span>
  <span class="n">game</span><span class="o">.</span><span class="n">payout</span><span class="p">(</span><span class="n">winners</span><span class="p">)</span>
  <span class="k">if</span> <span class="n">verbose</span><span class="p">:</span>
    <span class="n">game</span><span class="o">.</span><span class="n">print_cards</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now we got a well-defined game, all packed up in one function. However, in order to accomplish this, we had to reduce the number of actions that a player can perform to one single line. Our current players don't <code>bet()</code>, <code>raise_bet()</code>, or <code>fold</code>, they only play <code>cur_player.strategy(game)</code>. This might look like a restriction at first, but it's actually precisely what we want for our automatized Poker bots (and as you will see later, it also won't stop a human player from joining the game).</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Automatize-the-game-and-introduce-Player-bots">Automatize the game and introduce Player bots<a class="anchor-link" href="#Automatize-the-game-and-introduce-Player-bots">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now we can define our first Poker Bots. This is super easy: We only have to define some class (e.g. <code>class ÀutoPlayer</code>), which inherits from our player class. The only thing we have to write out is our <code>game.strategy()</code> given our players and our games.
Let's start with two super simple player bots: <code>AutoPlayer</code>, which simply tries to call all the time (or else plays random) and <code>ComparingPlayer</code>, which raises if it can form a combination that's not already present in the open cards.</p>
<p>We also can introduce cheating Player classes (e.g. <code>AllmightyPlayer</code>), which can look into some or all cards from the other players. However, obvisouly we want to derive Poker algorithms that can succeed without cheating.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">class</span> <span class="nc">AutoPlayer</span><span class="p">(</span><span class="n">Player</span><span class="p">):</span>
  <span class="k">def</span> <span class="nf">strategy</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">game</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;A strategy that always calls or if first, randomly raises or folds.&quot;&quot;&quot;</span>
    <span class="n">max_stakes</span> <span class="o">=</span> <span class="nb">max</span><span class="p">([</span><span class="n">player</span><span class="o">.</span><span class="n">stakes</span> <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">game</span><span class="o">.</span><span class="n">players</span><span class="p">])</span>
    <span class="c1"># if it&#39;s possible to call, call.</span>
    <span class="k">if</span> <span class="n">max_stakes</span> <span class="o">&gt;</span> <span class="bp">self</span><span class="o">.</span><span class="n">stakes</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">call</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
      <span class="c1"># else randomly raise or fold</span>
      <span class="k">if</span> <span class="nb">bool</span><span class="p">(</span><span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span><span class="mi">1</span><span class="p">)):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">raise_bet</span><span class="p">(</span><span class="n">game</span><span class="p">,</span> <span class="mi">50</span><span class="p">)</span>
      <span class="k">else</span><span class="p">:</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">check</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>


<span class="k">class</span> <span class="nc">ComparingPlayer</span><span class="p">(</span><span class="n">Player</span><span class="p">):</span>
  <span class="k">def</span> <span class="nf">strategy</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">game</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;A strategy that raises when its combo is better than the open combo.&quot;&quot;&quot;</span>

    <span class="c1"># define the worth of the player&#39;s combo and the open combo</span>
    <span class="n">combo</span><span class="p">,</span> <span class="n">determinant</span> <span class="o">=</span> <span class="n">score</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">cards</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span> <span class="o">+</span> <span class="n">game</span><span class="o">.</span><span class="n">open_cards</span><span class="p">())</span>
    <span class="k">if</span> <span class="nb">len</span><span class="p">(</span><span class="n">game</span><span class="o">.</span><span class="n">open_cards</span><span class="p">())</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
      <span class="n">open_combo</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="k">else</span><span class="p">:</span>
      <span class="n">open_combo</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">score</span><span class="p">(</span><span class="n">game</span><span class="o">.</span><span class="n">open_cards</span><span class="p">())</span>

    <span class="c1"># bet only if better than the open combo else call</span>
    <span class="k">if</span> <span class="n">combo</span> <span class="o">&gt;</span> <span class="n">open_combo</span> <span class="ow">and</span> <span class="bp">self</span><span class="o">.</span><span class="n">stakes</span> <span class="o">&lt;</span> <span class="mi">200</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">raise_bet</span><span class="p">(</span><span class="n">game</span><span class="p">,</span> <span class="mi">50</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">call</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>

<span class="k">class</span> <span class="nc">AllmightyPlayer</span><span class="p">(</span><span class="n">Player</span><span class="p">):</span>
  <span class="k">def</span> <span class="nf">strategy</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">game</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;A cheating Player that already knows who will win the game.&quot;&quot;&quot;</span>
    <span class="c1"># bet if player would win with the given cards, else call</span>
    <span class="k">if</span> <span class="bp">self</span> <span class="ow">in</span> <span class="n">game</span><span class="o">.</span><span class="n">showdown</span><span class="p">():</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">raise_bet</span><span class="p">(</span><span class="n">game</span><span class="p">,</span> <span class="mi">50</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">call</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>You see that defining a poker algorithm can be extremely easy. Feel free to create your own strategies and test them out later...</p>
<p>For now, let's start a game with two AutoPlayers and one ComparingPlayer and see how it looks.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">joe</span> <span class="o">=</span> <span class="n">AutoPlayer</span><span class="p">(</span><span class="s2">&quot;Joe&quot;</span><span class="p">,</span> <span class="mi">50</span><span class="p">)</span>
<span class="n">audrey</span> <span class="o">=</span> <span class="n">AutoPlayer</span><span class="p">(</span><span class="s2">&quot;Audrey&quot;</span><span class="p">,</span> <span class="mi">50</span><span class="p">)</span>
<span class="n">janet</span> <span class="o">=</span> <span class="n">ComparingPlayer</span><span class="p">(</span><span class="s2">&quot;Janet&quot;</span><span class="p">,</span> <span class="mi">50</span><span class="p">)</span>

<span class="n">players</span> <span class="o">=</span> <span class="p">[</span><span class="n">joe</span><span class="p">,</span> <span class="n">audrey</span><span class="p">,</span> <span class="n">janet</span><span class="p">]</span>
<span class="n">run_game</span><span class="p">(</span><span class="n">players</span><span class="p">,</span> <span class="n">small_blind</span><span class="o">=</span><span class="mf">0.1</span><span class="p">,</span> <span class="n">big_blind</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
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
Pre-Flop

Game starts. Small blind: Audrey; Big blind: Janet
Audrey added 0.1 to the pot. Player money=49.9; Pot money=0.1
Janet added 0.2 to the pot. Player money=49.8; Pot money=0.30000000000000004
Joe called.
Joe added 0.2 to the pot. Player money=49.8; Pot money=0.5
Audrey called.
Audrey added 0.1 to the pot. Player money=49.8; Pot money=0.6
Janet called.
Janet added 0.0 to the pot. Player money=49.8; Pot money=0.6

Flop
Open cards after flop: [(5, &#39;diamonds&#39;), (10, &#39;hearts&#39;), (&#39;K&#39;, &#39;hearts&#39;)]
Joe raised the bet by 50.
Joe added 50.0 to the pot. Player money=-0.20000000000000284; Pot money=50.6
Audrey called.
Audrey added 50.0 to the pot. Player money=-0.20000000000000284; Pot money=100.6
Janet called.
Janet added 50.0 to the pot. Player money=-0.20000000000000284; Pot money=150.6

River
Open cards after river: [(5, &#39;diamonds&#39;), (10, &#39;hearts&#39;), (&#39;K&#39;, &#39;hearts&#39;), (&#39;J&#39;, &#39;clubs&#39;)]
Joe raised the bet by 50.
Joe added 50.0 to the pot. Player money=-50.2; Pot money=200.6
Audrey called.
Audrey added 50.0 to the pot. Player money=-50.2; Pot money=250.6
Janet called.
Janet added 50.0 to the pot. Player money=-50.2; Pot money=300.6

Turn
Open cards after turn: [(5, &#39;diamonds&#39;), (10, &#39;hearts&#39;), (&#39;K&#39;, &#39;hearts&#39;), (&#39;J&#39;, &#39;clubs&#39;), (&#39;J&#39;, &#39;diamonds&#39;)]
Joe raised the bet by 50.
Joe added 50.0 to the pot. Player money=-100.2; Pot money=350.6
Audrey called.
Audrey added 49.999999999999986 to the pot. Player money=-100.19999999999999; Pot money=400.6
Janet called.
Janet added 49.999999999999986 to the pot. Player money=-100.19999999999999; Pot money=450.6
Best cards: [&#39;Janet&#39;] (Pair with J)

Janet took the pot of 450.6 and has now 350.40000000000003 in stock.

Public cards:  [(5, &#39;diamonds&#39;), (10, &#39;hearts&#39;), (&#39;K&#39;, &#39;hearts&#39;), (&#39;J&#39;, &#39;clubs&#39;), (&#39;J&#39;, &#39;diamonds&#39;)]
Player cards: 
	Joe: [(6, &#39;spades&#39;), (3, &#39;clubs&#39;)]
	Audrey: [(2, &#39;hearts&#39;), (7, &#39;clubs&#39;)]
	Janet: [(7, &#39;spades&#39;), (9, &#39;spades&#39;)]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>As you can see, there's not much action in this game. It's mostly just calling. However, some times it will occur that Janet (the <code>ComparingPlayer</code>) massively outbets the other two players. Let's see how they compare on the long run. In the next block, we will simulate a large number of games, while logging the player money. Afterwards, we plot them to see how they performed in comparison.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># define the players</span>
<span class="n">joe</span> <span class="o">=</span> <span class="n">AutoPlayer</span><span class="p">(</span><span class="s2">&quot;Joe&quot;</span><span class="p">,</span> <span class="mi">1000</span><span class="p">)</span>
<span class="n">audrey</span> <span class="o">=</span> <span class="n">AutoPlayer</span><span class="p">(</span><span class="s2">&quot;Audrey&quot;</span><span class="p">,</span> <span class="mi">1000</span><span class="p">)</span>
<span class="n">janet</span> <span class="o">=</span> <span class="n">ComparingPlayer</span><span class="p">(</span><span class="s2">&quot;Janet&quot;</span><span class="p">,</span> <span class="mi">1000</span><span class="p">)</span>
<span class="n">players</span> <span class="o">=</span> <span class="p">[</span><span class="n">joe</span><span class="p">,</span> <span class="n">audrey</span><span class="p">,</span> <span class="n">janet</span><span class="p">]</span>

<span class="c1"># loop through 1000 poker games while logging the player money</span>
<span class="n">stock_log</span> <span class="o">=</span> <span class="p">{</span><span class="n">player</span><span class="o">.</span><span class="n">name</span><span class="p">:[]</span> <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">players</span><span class="p">}</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">1000</span><span class="p">):</span>
  
  <span class="c1"># iterate through the players to switch starting positions</span>
  <span class="n">players</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">players</span><span class="o">.</span><span class="n">pop</span><span class="p">(</span><span class="mi">0</span><span class="p">))</span>

  <span class="c1"># run a new game</span>
  <span class="n">run_game</span><span class="p">(</span><span class="n">players</span><span class="p">,</span> <span class="n">small_blind</span><span class="o">=</span><span class="mf">0.1</span><span class="p">,</span> <span class="n">big_blind</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

  <span class="c1"># log their wins/losses</span>
  <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">players</span><span class="p">:</span>
    <span class="n">stock_log</span><span class="p">[</span><span class="n">player</span><span class="o">.</span><span class="n">name</span><span class="p">]</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">player</span><span class="o">.</span><span class="n">stock</span><span class="p">)</span>

<span class="c1"># plot the wins/losses</span>
<span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">players</span><span class="p">:</span>
  <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">stock_log</span><span class="p">[</span><span class="n">player</span><span class="o">.</span><span class="n">name</span><span class="p">])</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">([</span><span class="n">player</span><span class="o">.</span><span class="n">name</span> <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">players</span><span class="p">])</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;Poker rounds&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;Money in stock&quot;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[12]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Text(0, 0.5, &#39;Money in stock&#39;)</pre>
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
<p>We see that Janet's comparing strategy significantly outperforms the calling strategy over a large range of time. However both strategy are extremely simple and wouldn't stand a chance against a human player. So, let's make them more sophisticated by teaching them the wonders of probability theory...</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Probabilistic-Players">Probabilistic Players<a class="anchor-link" href="#Probabilistic-Players">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>First of all, we have to define a function that calculates our winning probability. This time, we do not want to peek into other people's cards, but instead estimate our chance of winning the game given our hand and all the possible combinations of cards unknown to us.</p>
<p>Theoretically, there are ${52 \choose 7} = 133784560$ possible card combinations in Texas Holdem Poker, which is simply a too large amount if you want to compare between all of them. You can usually drastically downsize this number by ignoring the fact that there are four different suits, however doing this while at the same time including Flush and Straight Flush combinations will result in relatively complicated functions. Here I settled for a Monte-Carlo-type estimation approach, which gives reasonable approximations to the true winning probability over a certain number of samples.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">approx_winning_prob</span><span class="p">(</span><span class="n">player_cards</span><span class="p">,</span> <span class="n">open_cards</span><span class="p">,</span> <span class="n">n_opponents</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span>
                        <span class="n">n_samples</span><span class="o">=</span><span class="mi">2000</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;Approximate winning probability at turn by comparing to random draws.&quot;&quot;&quot;</span>

  <span class="n">wins</span> <span class="o">=</span> <span class="mi">0</span>
  <span class="n">total</span> <span class="o">=</span> <span class="mi">0</span>
  <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_samples</span><span class="p">):</span>

    <span class="c1"># we cannot use the game deck, but make a new deck without the cards we know</span>
    <span class="n">deck</span> <span class="o">=</span> <span class="n">new_deck</span><span class="p">()</span>
    <span class="k">for</span> <span class="n">card</span> <span class="ow">in</span> <span class="n">player_cards</span> <span class="o">+</span> <span class="n">open_cards</span><span class="p">:</span>
      <span class="n">deck</span><span class="o">.</span><span class="n">remove</span><span class="p">(</span><span class="n">card</span><span class="p">)</span>

    <span class="c1"># We randomly draw the remaining public and opponents cards</span>
    <span class="n">test_cards</span> <span class="o">=</span> <span class="n">open_cards</span> <span class="o">+</span> <span class="p">[</span><span class="n">deck</span><span class="o">.</span><span class="n">pop</span><span class="p">()</span> <span class="k">for</span> <span class="n">c</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">5</span> <span class="o">-</span> <span class="nb">len</span><span class="p">(</span><span class="n">open_cards</span><span class="p">))]</span>
    <span class="n">opponent_cards</span> <span class="o">=</span> <span class="p">[</span><span class="n">deck</span><span class="o">.</span><span class="n">pop</span><span class="p">()</span> <span class="k">for</span> <span class="n">c</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">2</span><span class="p">)]</span>

    <span class="c1"># compare scores for hands and component</span>
    <span class="n">h_combo</span><span class="p">,</span> <span class="n">h_det</span> <span class="o">=</span> <span class="n">score</span><span class="p">(</span><span class="n">player_cards</span> <span class="o">+</span> <span class="n">test_cards</span><span class="p">)</span>
    <span class="n">o_combo</span><span class="p">,</span> <span class="n">o_det</span> <span class="o">=</span> <span class="n">score</span><span class="p">(</span><span class="n">opponent_cards</span> <span class="o">+</span> <span class="n">test_cards</span><span class="p">)</span>
    <span class="k">if</span> <span class="n">h_combo</span> <span class="o">&gt;</span> <span class="n">o_combo</span><span class="p">:</span>
      <span class="n">wins</span> <span class="o">+=</span> <span class="mi">1</span>
    <span class="k">elif</span> <span class="n">h_combo</span> <span class="o">==</span> <span class="n">o_combo</span> <span class="ow">and</span> <span class="n">h_det</span> <span class="o">&gt;</span> <span class="n">o_det</span><span class="p">:</span>
      <span class="n">wins</span> <span class="o">+=</span> <span class="mi">1</span>

    <span class="n">total</span> <span class="o">+=</span> <span class="mi">1</span>

  <span class="c1"># the probability of our hand winning against *one* unknown hand is:</span>
  <span class="n">p_win</span> <span class="o">=</span> <span class="n">wins</span> <span class="o">/</span> <span class="n">total</span>

  <span class="c1"># now we need to get the probability of winning against *all* opponents</span>
  <span class="k">return</span> <span class="n">p_win</span> <span class="o">**</span> <span class="n">n_opponents</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now we can define our first "smart" probabilistic players. Let's call the first <code>ProbabilisticPlayer</code>. It will place a large bet whenenver its own chances of winning are larger than the chances of their opponents. If their chances are slightly worse than their opponents' chances they will call, if they are substantially worse, they will fold. Another class could be the <code>RationalPlayer</code>. This one will fold only for a very low winning probability of $p_{(win)} &lt; 0.05$. Else, it will raise in relation to its winning probability, namely by $bet = {p_{(win)}}^2 * 100$, so with a $p_{(win)}=0.1$, it will raise by $bet = 0.1^2 * 100 = 1$, with a $p_{(win)}=0.9$, it will raise by $bet = 0.1^2 * 100 = 81$.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">class</span> <span class="nc">ProbabilisticPlayer</span><span class="p">(</span><span class="n">Player</span><span class="p">):</span>
  <span class="k">def</span> <span class="nf">strategy</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">game</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Raise if you&#39;re more likely to win than your opponents&quot;&quot;&quot;</span>
    <span class="c1"># calculate our own against all other winning probabilities</span>
    <span class="n">n_opponents</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">game</span><span class="o">.</span><span class="n">players_in</span><span class="p">())</span> <span class="o">-</span> <span class="mi">1</span>
    <span class="n">p_win</span> <span class="o">=</span> <span class="n">approx_winning_prob</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">cards</span><span class="p">,</span> <span class="n">game</span><span class="o">.</span><span class="n">open_cards</span><span class="p">(),</span> <span class="n">n_opponents</span><span class="p">,</span> <span class="mi">300</span><span class="p">)</span>
    <span class="n">p_win_op</span> <span class="o">=</span> <span class="p">(</span><span class="mi">1</span> <span class="o">-</span> <span class="n">p_win</span><span class="p">)</span> <span class="o">/</span> <span class="n">n_opponents</span>
    
    <span class="c1"># raise if you have better chances than others, until a max threshold</span>
    <span class="k">if</span> <span class="n">p_win</span> <span class="o">&gt;</span> <span class="n">p_win_op</span> <span class="ow">and</span> <span class="bp">self</span><span class="o">.</span><span class="n">stakes</span> <span class="o">&lt;</span> <span class="mi">200</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">raise_bet</span><span class="p">(</span><span class="n">game</span><span class="p">,</span> <span class="mi">50</span><span class="p">)</span>
    <span class="k">elif</span> <span class="n">p_win</span> <span class="o">&lt;</span> <span class="p">(</span><span class="n">p_win_op</span> <span class="o">-</span> <span class="mf">0.1</span><span class="p">):</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">fold</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">call</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>


<span class="k">class</span> <span class="nc">RationalPlayer</span><span class="p">(</span><span class="n">Player</span><span class="p">):</span>

  <span class="k">def</span> <span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">name</span><span class="p">,</span> <span class="n">stock</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Define some additional attributes to keep track of the number of bets&quot;&quot;&quot;</span>
    <span class="nb">super</span><span class="p">()</span><span class="o">.</span><span class="fm">__init__</span><span class="p">(</span><span class="n">name</span><span class="p">,</span> <span class="n">stock</span><span class="p">)</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">n_bets</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">betting_round</span> <span class="o">=</span> <span class="mi">0</span>

  <span class="k">def</span> <span class="nf">strategy</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">game</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Fold for very bad cards, else raise in relation to your winning prob&quot;&quot;&quot;</span>
    <span class="c1"># reset the number of bets in each betting round</span>
    <span class="k">if</span> <span class="n">game</span><span class="o">.</span><span class="n">current_state</span> <span class="o">!=</span> <span class="bp">self</span><span class="o">.</span><span class="n">betting_round</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">betting_round</span> <span class="o">=</span> <span class="n">game</span><span class="o">.</span><span class="n">current_state</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">n_bets</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="k">else</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">n_bets</span> <span class="o">+=</span> <span class="mi">1</span>

    <span class="c1"># calculate our against all other probabilities</span>
    <span class="n">n_opponents</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">game</span><span class="o">.</span><span class="n">players_in</span><span class="p">())</span> <span class="o">-</span> <span class="mi">1</span>
    <span class="n">p_win</span> <span class="o">=</span> <span class="n">approx_winning_prob</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">cards</span><span class="p">,</span> <span class="n">game</span><span class="o">.</span><span class="n">open_cards</span><span class="p">(),</span> <span class="n">n_opponents</span><span class="p">,</span> <span class="mi">300</span><span class="p">)</span>

    <span class="c1"># bet in relation to your winning probability, for 2 bets at most</span>
    <span class="k">if</span> <span class="n">p_win</span> <span class="o">&lt;</span> <span class="mf">0.05</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">fold</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>
    <span class="k">elif</span> <span class="bp">self</span><span class="o">.</span><span class="n">n_bets</span> <span class="o">&lt;</span> <span class="mi">2</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">raise_bet</span><span class="p">(</span><span class="n">game</span><span class="p">,</span> <span class="n">p_win</span><span class="o">**</span><span class="mi">2</span> <span class="o">*</span> <span class="mi">100</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">call</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Let's simulate the performance of our probabilistic players against the <code>ComparingPlayers</code>, which "excelled" in our earlier games.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">joe</span> <span class="o">=</span> <span class="n">ComparingPlayer</span><span class="p">(</span><span class="s2">&quot;Joe&quot;</span><span class="p">,</span> <span class="mi">100</span><span class="p">)</span>
<span class="n">audrey</span> <span class="o">=</span> <span class="n">ComparingPlayer</span><span class="p">(</span><span class="s2">&quot;Audrey&quot;</span><span class="p">,</span> <span class="mi">100</span><span class="p">)</span>
<span class="n">janet</span> <span class="o">=</span> <span class="n">RationalPlayer</span><span class="p">(</span><span class="s2">&quot;Janet&quot;</span><span class="p">,</span> <span class="mi">100</span><span class="p">)</span>
<span class="n">fred</span> <span class="o">=</span> <span class="n">RationalPlayer</span><span class="p">(</span><span class="s2">&quot;Fred&quot;</span><span class="p">,</span> <span class="mi">100</span><span class="p">)</span>
<span class="n">lobot</span> <span class="o">=</span> <span class="n">ProbabilisticPlayer</span><span class="p">(</span><span class="s2">&quot;Lobot&quot;</span><span class="p">,</span> <span class="mi">100</span><span class="p">)</span>
<span class="n">hailey</span> <span class="o">=</span> <span class="n">ProbabilisticPlayer</span><span class="p">(</span><span class="s2">&quot;Hailey&quot;</span><span class="p">,</span> <span class="mi">100</span><span class="p">)</span>

<span class="n">players</span> <span class="o">=</span> <span class="p">[</span><span class="n">joe</span><span class="p">,</span> <span class="n">audrey</span><span class="p">,</span> <span class="n">janet</span><span class="p">,</span> <span class="n">fred</span><span class="p">,</span> <span class="n">lobot</span><span class="p">,</span> <span class="n">hailey</span><span class="p">]</span>

<span class="n">stock_log</span> <span class="o">=</span> <span class="p">{</span><span class="n">player</span><span class="o">.</span><span class="n">name</span><span class="p">:[]</span> <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">players</span><span class="p">}</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">1000</span><span class="p">):</span>
  
  <span class="c1"># switch through the players:</span>
  <span class="n">players</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">players</span><span class="o">.</span><span class="n">pop</span><span class="p">(</span><span class="mi">0</span><span class="p">))</span>

  <span class="c1"># run a new game</span>
  <span class="k">if</span> <span class="n">i</span> <span class="o">%</span> <span class="mi">50</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Round: &quot;</span><span class="p">,</span> <span class="n">i</span><span class="p">)</span>
  <span class="n">run_game</span><span class="p">(</span><span class="n">players</span><span class="p">,</span> <span class="n">small_blind</span><span class="o">=</span><span class="mf">0.1</span><span class="p">,</span> <span class="n">big_blind</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

  <span class="c1"># log their wins/losses</span>
  <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">players</span><span class="p">:</span>
    <span class="n">stock_log</span><span class="p">[</span><span class="n">player</span><span class="o">.</span><span class="n">name</span><span class="p">]</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">player</span><span class="o">.</span><span class="n">stock</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Round:  0
Round:  50
Round:  100
Round:  150
Round:  200
Round:  250
Round:  300
Round:  350
Round:  400
Round:  450
Round:  500
Round:  550
Round:  600
Round:  650
Round:  700
Round:  750
Round:  800
Round:  850
Round:  900
Round:  950
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># plot the results</span>
<span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">players</span><span class="p">:</span>
  <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">stock_log</span><span class="p">[</span><span class="n">player</span><span class="o">.</span><span class="n">name</span><span class="p">])</span>

<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">([</span><span class="n">player</span><span class="o">.</span><span class="n">name</span> <span class="k">for</span> <span class="n">player</span> <span class="ow">in</span> <span class="n">players</span><span class="p">])</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;Poker rounds&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;Money in stock&quot;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[16]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Text(0, 0.5, &#39;Money in stock&#39;)</pre>
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
<p>As expected, our probabilistic players perform drastically better than our simple AutoPlayers due to precisely "knowing what to throw away, and knowing what to keep". We also see that the <code>RationalPlayer</code> class performs still a good bit better than the <code>ProbabilisticPlayer</code>, probably due to their ability of scaling their bets directly with their risks.
But how will these algorithms perform against a human player? Let's find it out by actually playing against our Poker bots by yourself...</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Your-turn:-Play-against-the-bots">Your turn: Play against the bots<a class="anchor-link" href="#Your-turn:-Play-against-the-bots">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>We can crate a new <code>HumanPlayer</code> class and handle it in exactly the same way as our automated player classes. The only difference is that each time our strategy is called, we ask for a player input and you can decide if and how much you want to bet this round. To keep it simple, we will just say that an input of "f" or "fold" means to fold, while any integer/float input will be interpreted as a raise, with e.g. <code>2.5</code> being a raise/bet of 2.5 to the current pot and <code>0</code> translating into a call/check.</p>
<p>To make things easier, I also introduced the option to display the winning probability compared to opponent players (just as the probabilistic bots). If you initialize a player with <code>HumanPlayer(..., show_probs=True)</code>, the winning probabilities will be printed each time before taking an input.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">class</span> <span class="nc">HumanPlayer</span><span class="p">(</span><span class="n">Player</span><span class="p">):</span>

  <span class="k">def</span> <span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">name</span><span class="p">,</span> <span class="n">stock</span><span class="p">,</span> <span class="n">show_probs</span><span class="o">=</span><span class="kc">False</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Introduce an attribute for displaying/ignoring winning probabilities&quot;&quot;&quot;</span>
    <span class="nb">super</span><span class="p">()</span><span class="o">.</span><span class="fm">__init__</span><span class="p">(</span><span class="n">name</span><span class="p">,</span> <span class="n">stock</span><span class="p">)</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">show_probs</span> <span class="o">=</span> <span class="n">show_probs</span>

  <span class="k">def</span> <span class="nf">strategy</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">game</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Decide on a strategy via user input.&quot;&quot;&quot;</span>

    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Current pot: </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">game</span><span class="o">.</span><span class="n">pot</span><span class="p">))</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Open_cards: </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">game</span><span class="o">.</span><span class="n">open_cards</span><span class="p">()))</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Your cards: </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">cards</span><span class="p">))</span>
    <span class="k">if</span> <span class="bp">self</span><span class="o">.</span><span class="n">show_probs</span><span class="p">:</span>
      <span class="n">n_opponents</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">game</span><span class="o">.</span><span class="n">players_in</span><span class="p">())</span> <span class="o">-</span> <span class="mi">1</span>
      <span class="n">p_win</span> <span class="o">=</span> <span class="n">approx_winning_prob</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">cards</span><span class="p">,</span> <span class="n">game</span><span class="o">.</span><span class="n">open_cards</span><span class="p">(),</span> <span class="n">n_opponents</span><span class="p">)</span>
      <span class="n">p_win_op</span> <span class="o">=</span> <span class="p">(</span><span class="mi">1</span> <span class="o">-</span> <span class="n">p_win</span><span class="p">)</span> <span class="o">/</span> <span class="n">n_opponents</span>
      <span class="n">msg</span> <span class="o">=</span> <span class="s2">&quot;You vs. opponent winning probability: </span><span class="si">{0}</span><span class="s2"> : </span><span class="si">{1}</span><span class="s2">&quot;</span>
      <span class="nb">print</span><span class="p">(</span><span class="n">msg</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">p_win</span><span class="p">,</span> <span class="n">p_win_op</span><span class="p">))</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">Your choice:&quot;</span><span class="p">)</span>
    <span class="n">choice</span> <span class="o">=</span> <span class="nb">input</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">type &#39;fold&#39; to fold or any float to raise/bet (&#39;0&#39;=call/check): &quot;</span><span class="p">)</span>
    <span class="k">if</span> <span class="n">choice</span> <span class="ow">in</span> <span class="p">(</span><span class="s2">&quot;f&quot;</span><span class="p">,</span> <span class="s2">&quot;fold&quot;</span><span class="p">):</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">fold</span><span class="p">(</span><span class="n">game</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">raise_bet</span><span class="p">(</span><span class="n">game</span><span class="p">,</span> <span class="nb">float</span><span class="p">(</span><span class="n">choice</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now, let's define a bunch of players to play with:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">audrey</span> <span class="o">=</span> <span class="n">AutoPlayer</span><span class="p">(</span><span class="s2">&quot;Audrey&quot;</span><span class="p">,</span> <span class="mi">1000</span><span class="p">)</span>
<span class="n">janet</span> <span class="o">=</span> <span class="n">RationalPlayer</span><span class="p">(</span><span class="s2">&quot;Janet&quot;</span><span class="p">,</span> <span class="mi">1000</span><span class="p">)</span>
<span class="n">lobot</span> <span class="o">=</span> <span class="n">ProbabilisticPlayer</span><span class="p">(</span><span class="s2">&quot;Lobot&quot;</span><span class="p">,</span> <span class="mi">1000</span><span class="p">)</span>
<span class="n">you</span> <span class="o">=</span> <span class="n">HumanPlayer</span><span class="p">(</span><span class="s2">&quot;You&quot;</span><span class="p">,</span> <span class="mi">1000</span><span class="p">,</span> <span class="n">show_probs</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="n">players</span> <span class="o">=</span> <span class="p">[</span><span class="n">audrey</span><span class="p">,</span> <span class="n">janet</span><span class="p">,</span> <span class="n">lobot</span><span class="p">,</span> <span class="n">you</span><span class="p">]</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>And play a nice round of Poker with them. If you want to play another round, just re-run the following cell.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">run_game</span><span class="p">(</span><span class="n">players</span><span class="p">,</span> <span class="n">small_blind</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">big_blind</span><span class="o">=</span><span class="mi">20</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="c1"># cycle the player position for the next round</span>
<span class="n">players</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">players</span><span class="o">.</span><span class="n">pop</span><span class="p">(</span><span class="mi">0</span><span class="p">))</span>
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
Pre-Flop

Game starts. Small blind: Lobot; Big blind: You
Lobot added 10 to the pot. Player money=990; Pot money=10
You added 20 to the pot. Player money=980; Pot money=30
Audrey called.
Audrey added 20 to the pot. Player money=980; Pot money=50
Janet raised the bet by 1.0779215328999998.
Janet added 21.0779215329 to the pot. Player money=978.9220784671; Pot money=71.0779215329
Lobot folded.
Current pot: 71.0779215329
Open_cards: []
Your cards: [(4, &#39;hearts&#39;), (6, &#39;diamonds&#39;)]
You vs. opponent winning probability: 0.10562500000000001 : 0.4471875

Your choice:

type &#39;fold&#39; to fold or any float to raise/bet (&#39;0&#39;=call/check): 0
You raised the bet by 0.0.
You added 1.0779215328999996 to the pot. Player money=978.9220784671; Pot money=72.15584306580001
Audrey called.
Audrey added 1.0779215328999996 to the pot. Player money=978.9220784671; Pot money=73.23376459870002

Flop
Open cards after flop: [(8, &#39;hearts&#39;), (3, &#39;hearts&#39;), (4, &#39;spades&#39;)]
Audrey checked.
Janet raised the bet by 0.480865197530864.
Janet added 0.480865197530864 to the pot. Player money=978.4412132695692; Pot money=73.71462979623088
Current pot: 73.71462979623088
Open_cards: [(8, &#39;hearts&#39;), (3, &#39;hearts&#39;), (4, &#39;spades&#39;)]
Your cards: [(4, &#39;hearts&#39;), (6, &#39;diamonds&#39;)]
You vs. opponent winning probability: 0.34809999999999997 : 0.32595

Your choice:

type &#39;fold&#39; to fold or any float to raise/bet (&#39;0&#39;=call/check): 10
You raised the bet by 10.0.
You added 10.480865197530864 to the pot. Player money=968.4412132695692; Pot money=84.19549499376174
Audrey called.
Audrey added 10.480865197530864 to the pot. Player money=968.4412132695692; Pot money=94.6763601912926
Janet raised the bet by 0.7745955679012347.
Janet added 10.774595567901235 to the pot. Player money=967.666617701668; Pot money=105.45095575919383
Current pot: 105.45095575919383
Open_cards: [(8, &#39;hearts&#39;), (3, &#39;hearts&#39;), (4, &#39;spades&#39;)]
Your cards: [(4, &#39;hearts&#39;), (6, &#39;diamonds&#39;)]
You vs. opponent winning probability: 0.35700625 : 0.321496875

Your choice:

type &#39;fold&#39; to fold or any float to raise/bet (&#39;0&#39;=call/check): 10
You raised the bet by 10.0.
You added 10.774595567901233 to the pot. Player money=957.666617701668; Pot money=116.22555132709506
Audrey called.
Audrey added 10.774595567901233 to the pot. Player money=957.666617701668; Pot money=127.00014689499629
Janet called.
Janet added 10.0 to the pot. Player money=957.666617701668; Pot money=137.0001468949963

River
Open cards after river: [(8, &#39;hearts&#39;), (3, &#39;hearts&#39;), (4, &#39;spades&#39;), (10, &#39;clubs&#39;)]
Audrey raised the bet by 50.
Audrey added 50.0 to the pot. Player money=907.666617701668; Pot money=187.0001468949963
Janet raised the bet by 0.31372445679012345.
Janet added 50.313724456790126 to the pot. Player money=907.3528932448778; Pot money=237.31387135178642
Current pot: 237.31387135178642
Open_cards: [(8, &#39;hearts&#39;), (3, &#39;hearts&#39;), (4, &#39;spades&#39;), (10, &#39;clubs&#39;)]
Your cards: [(4, &#39;hearts&#39;), (6, &#39;diamonds&#39;)]
You vs. opponent winning probability: 0.31360000000000005 : 0.34319999999999995

Your choice:

type &#39;fold&#39; to fold or any float to raise/bet (&#39;0&#39;=call/check): 5
You raised the bet by 5.0.
You added 55.313724456790126 to the pot. Player money=902.3528932448778; Pot money=292.62759580857653
Audrey called.
Audrey added 5.313724456790126 to the pot. Player money=902.3528932448778; Pot money=297.94132026536664
Janet raised the bet by 0.390625.
Janet added 5.390625 to the pot. Player money=901.9622682448778; Pot money=303.33194526536664
Current pot: 303.33194526536664
Open_cards: [(8, &#39;hearts&#39;), (3, &#39;hearts&#39;), (4, &#39;spades&#39;), (10, &#39;clubs&#39;)]
Your cards: [(4, &#39;hearts&#39;), (6, &#39;diamonds&#39;)]
You vs. opponent winning probability: 0.31360000000000005 : 0.34319999999999995

Your choice:

type &#39;fold&#39; to fold or any float to raise/bet (&#39;0&#39;=call/check): 0
You raised the bet by 0.0.
You added 0.390625 to the pot. Player money=901.9622682448778; Pot money=303.72257026536664
Audrey called.
Audrey added 0.390625 to the pot. Player money=901.9622682448778; Pot money=304.11319526536664

Turn
Open cards after turn: [(8, &#39;hearts&#39;), (3, &#39;hearts&#39;), (4, &#39;spades&#39;), (10, &#39;clubs&#39;), (&#39;A&#39;, &#39;hearts&#39;)]
Audrey checked.
Janet folded.
Current pot: 304.11319526536664
Open_cards: [(8, &#39;hearts&#39;), (3, &#39;hearts&#39;), (4, &#39;spades&#39;), (10, &#39;clubs&#39;), (&#39;A&#39;, &#39;hearts&#39;)]
Your cards: [(4, &#39;hearts&#39;), (6, &#39;diamonds&#39;)]
You vs. opponent winning probability: 0.496 : 0.504

Your choice:

type &#39;fold&#39; to fold or any float to raise/bet (&#39;0&#39;=call/check): 0
You raised the bet by 0.0.
You added 0.0 to the pot. Player money=901.9622682448778; Pot money=304.11319526536664
Best cards: [&#39;You&#39;] (Pair with 4)

You took the pot of 304.11319526536664 and has now 1206.0754635102444 in stock.

Public cards:  [(8, &#39;hearts&#39;), (3, &#39;hearts&#39;), (4, &#39;spades&#39;), (10, &#39;clubs&#39;), (&#39;A&#39;, &#39;hearts&#39;)]
Player cards: 
	Audrey: [(&#39;K&#39;, &#39;clubs&#39;), (3, &#39;spades&#39;)]
	Janet: [(&#39;J&#39;, &#39;spades&#39;), (&#39;K&#39;, &#39;hearts&#39;)] (Folded)
	Lobot: [(3, &#39;clubs&#39;), (10, &#39;diamonds&#39;)] (Folded)
	You: [(4, &#39;hearts&#39;), (6, &#39;diamonds&#39;)]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>As you can see, these bots are still easy to trick and far from perfect. The framework we defined here allows numerous possible enhancements. For example, we could use statistics or machine learning to let players predict the cards of other players, based on their betting behaviour. We could use this framework and train more complex learning agents to produce human-level poker playing bots. However, for now I think it's a good idea to settle with what we've learned so far. We defined an entire Poker game, automated Players that can play it, and even competed against them. That should be enough for today. If you liked the notebook, stay tuned: I will follow up with a new notebook and some more refined Poker playing bots soon.</p>
<p>I hope this notebook has also left you with a nice impression of all the different things you can do with Python. I don't know about any other programming language that gives you so many elegant ways to produce extremely functional code, while at the same time being easily readable by humans. I hope you got the same impression after reading this.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<hr>
<p>BSD 3-Clause License</p>
<p>Copyright (c) 2020, Dirk Gütlin</p>
<p>All rights reserved.</p>

</div>
</div>
</div>
    </div>
  </div>
</body>

 


</html>

