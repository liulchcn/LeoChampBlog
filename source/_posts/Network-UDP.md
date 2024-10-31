---
title: Network UDP
date: 2024-11-01 07:26:33
tags:
layout: false
---

{% raw %}

<!doctype html>
<html>
<head>
<meta charset='UTF-8'><meta name='viewport' content='width=device-width initial-scale=1'>

<link href='https://fonts.googleapis.com/css?family=PT+Serif:400,400italic,700,700italic&subset=latin,cyrillic-ext,cyrillic,latin-ext' rel='stylesheet' type='text/css' /><style type='text/css'>html {overflow-x: initial !important;}:root { --bg-color:#ffffff; --text-color:#333333; --select-text-bg-color:#B5D6FC; --select-text-font-color:auto; --monospace:"Lucida Console",Consolas,"Courier",monospace; --title-bar-height:20px; }
.mac-os-11 { --title-bar-height:28px; }
html { font-size: 14px; background-color: var(--bg-color); color: var(--text-color); font-family: "Helvetica Neue", Helvetica, Arial, sans-serif; -webkit-font-smoothing: antialiased; }
h1, h2, h3, h4, h5 { white-space: pre-wrap; }
body { margin: 0px; padding: 0px; height: auto; inset: 0px; font-size: 1rem; line-height: 1.42857; overflow-x: hidden; background: inherit; }
iframe { margin: auto; }
a.url { word-break: break-all; }
a:active, a:hover { outline: 0px; }
.in-text-selection, ::selection { text-shadow: none; background: var(--select-text-bg-color); color: var(--select-text-font-color); }
#write { margin: 0px auto; height: auto; width: inherit; word-break: normal; overflow-wrap: break-word; position: relative; white-space: normal; overflow-x: visible; padding-top: 36px; }
#write.first-line-indent p { text-indent: 2em; }
#write.first-line-indent li p, #write.first-line-indent p * { text-indent: 0px; }
#write.first-line-indent li { margin-left: 2em; }
.for-image #write { padding-left: 8px; padding-right: 8px; }
body.typora-export { padding-left: 30px; padding-right: 30px; }
.typora-export .footnote-line, .typora-export li, .typora-export p { white-space: pre-wrap; }
.typora-export .task-list-item input { pointer-events: none; }
@media screen and (max-width: 500px) {
  body.typora-export { padding-left: 0px; padding-right: 0px; }
  #write { padding-left: 20px; padding-right: 20px; }
}
#write li > figure:last-child { margin-bottom: 0.5rem; }
#write ol, #write ul { position: relative; }
img { max-width: 100%; vertical-align: middle; image-orientation: from-image; }
button, input, select, textarea { color: inherit; font: inherit; }
input[type="checkbox"], input[type="radio"] { line-height: normal; padding: 0px; }
*, ::after, ::before { box-sizing: border-box; }
#write h1, #write h2, #write h3, #write h4, #write h5, #write h6, #write p, #write pre { width: inherit; }
#write h1, #write h2, #write h3, #write h4, #write h5, #write h6, #write p { position: relative; }
p { line-height: inherit; }
h1, h2, h3, h4, h5, h6 { break-after: avoid-page; break-inside: avoid; orphans: 4; }
p { orphans: 4; }
h1 { font-size: 2rem; }
h2 { font-size: 1.8rem; }
h3 { font-size: 1.6rem; }
h4 { font-size: 1.4rem; }
h5 { font-size: 1.2rem; }
h6 { font-size: 1rem; }
.md-math-block, .md-rawblock, h1, h2, h3, h4, h5, h6, p { margin-top: 1rem; margin-bottom: 1rem; }
.hidden { display: none; }
.md-blockmeta { color: rgb(204, 204, 204); font-weight: 700; font-style: italic; }
a { cursor: pointer; }
sup.md-footnote { padding: 2px 4px; background-color: rgba(238, 238, 238, 0.7); color: rgb(85, 85, 85); border-radius: 4px; cursor: pointer; }
sup.md-footnote a, sup.md-footnote a:hover { color: inherit; text-transform: inherit; text-decoration: inherit; }
#write input[type="checkbox"] { cursor: pointer; width: inherit; height: inherit; }
figure { overflow-x: auto; margin: 1.2em 0px; max-width: calc(100% + 16px); padding: 0px; }
figure > table { margin: 0px; }
thead, tr { break-inside: avoid; break-after: auto; }
thead { display: table-header-group; }
table { border-collapse: collapse; border-spacing: 0px; width: 100%; overflow: auto; break-inside: auto; text-align: left; }
table.md-table td { min-width: 32px; }
.CodeMirror-gutters { border-right: 0px; background-color: inherit; }
.CodeMirror-linenumber { user-select: none; }
.CodeMirror { text-align: left; }
.CodeMirror-placeholder { opacity: 0.3; }
.CodeMirror pre { padding: 0px 4px; }
.CodeMirror-lines { padding: 0px; }
div.hr:focus { cursor: none; }
#write pre { white-space: pre-wrap; }
#write.fences-no-line-wrapping pre { white-space: pre; }
#write pre.ty-contain-cm { white-space: normal; }
.CodeMirror-gutters { margin-right: 4px; }
.md-fences { font-size: 0.9rem; display: block; break-inside: avoid; text-align: left; overflow: visible; white-space: pre; background: inherit; position: relative !important; }
.md-fences-adv-panel { width: 100%; margin-top: 10px; text-align: center; padding-top: 0px; padding-bottom: 8px; overflow-x: auto; }
#write .md-fences.mock-cm { white-space: pre-wrap; }
.md-fences.md-fences-with-lineno { padding-left: 0px; }
#write.fences-no-line-wrapping .md-fences.mock-cm { white-space: pre; overflow-x: auto; }
.md-fences.mock-cm.md-fences-with-lineno { padding-left: 8px; }
.CodeMirror-line, twitterwidget { break-inside: avoid; }
svg { break-inside: avoid; }
.footnotes { opacity: 0.8; font-size: 0.9rem; margin-top: 1em; margin-bottom: 1em; }
.footnotes + .footnotes { margin-top: 0px; }
.md-reset { margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: top; background: 0px 0px; text-decoration: none; text-shadow: none; float: none; position: static; width: auto; height: auto; white-space: nowrap; cursor: inherit; -webkit-tap-highlight-color: transparent; line-height: normal; font-weight: 400; text-align: left; box-sizing: content-box; direction: ltr; }
li div { padding-top: 0px; }
blockquote { margin: 1rem 0px; }
li .mathjax-block, li p { margin: 0.5rem 0px; }
li blockquote { margin: 1rem 0px; }
li { margin: 0px; position: relative; }
blockquote > :last-child { margin-bottom: 0px; }
blockquote > :first-child, li > :first-child { margin-top: 0px; }
.footnotes-area { color: rgb(136, 136, 136); margin-top: 0.714rem; padding-bottom: 0.143rem; white-space: normal; }
#write .footnote-line { white-space: pre-wrap; }
@media print {
  body, html { border: 1px solid transparent; height: 99%; break-after: avoid; break-before: avoid; font-variant-ligatures: no-common-ligatures; }
  #write { margin-top: 0px; border-color: transparent !important; padding-top: 0px !important; padding-bottom: 0px !important; }
  .typora-export * { -webkit-print-color-adjust: exact; }
  .typora-export #write { break-after: avoid; }
  .typora-export #write::after { height: 0px; }
  .is-mac table { break-inside: avoid; }
  #write > p:nth-child(1) { margin-top: 0px; }
  .typora-export-show-outline .typora-export-sidebar { display: none; }
  figure { overflow-x: visible; }
}
.footnote-line { margin-top: 0.714em; font-size: 0.7em; }
a img, img a { cursor: pointer; }
pre.md-meta-block { font-size: 0.8rem; min-height: 0.8rem; white-space: pre-wrap; background: rgb(204, 204, 204); display: block; overflow-x: hidden; }
p > .md-image:only-child:not(.md-img-error) img, p > img:only-child { display: block; margin: auto; }
#write.first-line-indent p > .md-image:only-child:not(.md-img-error) img { left: -2em; position: relative; }
p > .md-image:only-child { display: inline-block; width: 100%; }
#write .MathJax_Display { margin: 0.8em 0px 0px; }
.md-math-block { width: 100%; }
.md-math-block:not(:empty)::after { display: none; }
.MathJax_ref { fill: currentcolor; }
[contenteditable="true"]:active, [contenteditable="true"]:focus, [contenteditable="false"]:active, [contenteditable="false"]:focus { outline: 0px; box-shadow: none; }
.md-task-list-item { position: relative; list-style-type: none; }
.task-list-item.md-task-list-item { padding-left: 0px; }
.md-task-list-item > input { position: absolute; top: 0px; left: 0px; margin-left: -1.2em; margin-top: calc(1em - 10px); border: none; }
.math { font-size: 1rem; }
.md-toc { min-height: 3.58rem; position: relative; font-size: 0.9rem; border-radius: 10px; }
.md-toc-content { position: relative; margin-left: 0px; }
.md-toc-content::after, .md-toc::after { display: none; }
.md-toc-item { display: block; color: rgb(65, 131, 196); }
.md-toc-item a { text-decoration: none; }
.md-toc-inner:hover { text-decoration: underline; }
.md-toc-inner { display: inline-block; cursor: pointer; }
.md-toc-h1 .md-toc-inner { margin-left: 0px; font-weight: 700; }
.md-toc-h2 .md-toc-inner { margin-left: 2em; }
.md-toc-h3 .md-toc-inner { margin-left: 4em; }
.md-toc-h4 .md-toc-inner { margin-left: 6em; }
.md-toc-h5 .md-toc-inner { margin-left: 8em; }
.md-toc-h6 .md-toc-inner { margin-left: 10em; }
@media screen and (max-width: 48em) {
  .md-toc-h3 .md-toc-inner { margin-left: 3.5em; }
  .md-toc-h4 .md-toc-inner { margin-left: 5em; }
  .md-toc-h5 .md-toc-inner { margin-left: 6.5em; }
  .md-toc-h6 .md-toc-inner { margin-left: 8em; }
}
a.md-toc-inner { font-size: inherit; font-style: inherit; font-weight: inherit; line-height: inherit; }
.footnote-line a:not(.reversefootnote) { color: inherit; }
.reversefootnote { font-family: ui-monospace, sans-serif; }
.md-attr { display: none; }
.md-fn-count::after { content: "."; }
code, pre, samp, tt { font-family: var(--monospace); }
kbd { margin: 0px 0.1em; padding: 0.1em 0.6em; font-size: 0.8em; color: rgb(36, 39, 41); background: rgb(255, 255, 255); border: 1px solid rgb(173, 179, 185); border-radius: 3px; box-shadow: rgba(12, 13, 14, 0.2) 0px 1px 0px, rgb(255, 255, 255) 0px 0px 0px 2px inset; white-space: nowrap; vertical-align: middle; }
.md-comment { color: rgb(162, 127, 3); opacity: 0.6; font-family: var(--monospace); }
code { text-align: left; vertical-align: initial; }
a.md-print-anchor { white-space: pre !important; border-width: initial !important; border-style: none !important; border-color: initial !important; display: inline-block !important; position: absolute !important; width: 1px !important; right: 0px !important; outline: 0px !important; background: 0px 0px !important; text-decoration: initial !important; text-shadow: initial !important; }
.os-windows.monocolor-emoji .md-emoji { font-family: "Segoe UI Symbol", sans-serif; }
.md-diagram-panel > svg { max-width: 100%; }
[lang="flow"] svg, [lang="mermaid"] svg { max-width: 100%; height: auto; }
[lang="mermaid"] .node text { font-size: 1rem; }
table tr th { border-bottom: 0px; }
video { max-width: 100%; display: block; margin: 0px auto; }
iframe { max-width: 100%; width: 100%; border: none; }
.highlight td, .highlight tr { border: 0px; }
mark { background: rgb(255, 255, 0); color: rgb(0, 0, 0); }
.md-html-inline .md-plain, .md-html-inline strong, mark .md-inline-math, mark strong { color: inherit; }
.md-expand mark .md-meta { opacity: 0.3 !important; }
mark .md-meta { color: rgb(0, 0, 0); }
@media print {
  .typora-export h1, .typora-export h2, .typora-export h3, .typora-export h4, .typora-export h5, .typora-export h6 { break-inside: avoid; }
}
.md-diagram-panel .messageText { stroke: none !important; }
.md-diagram-panel .start-state { fill: var(--node-fill); }
.md-diagram-panel .edgeLabel rect { opacity: 1 !important; }
.md-fences.md-fences-math { font-size: 1em; }
.md-fences-advanced:not(.md-focus) { padding: 0px; white-space: nowrap; border: 0px; }
.md-fences-advanced:not(.md-focus) { background: inherit; }
.typora-export-show-outline .typora-export-content { max-width: 1440px; margin: auto; display: flex; flex-direction: row; }
.typora-export-sidebar { width: 300px; font-size: 0.8rem; margin-top: 80px; margin-right: 18px; }
.typora-export-show-outline #write { --webkit-flex:2; flex: 2 1 0%; }
.typora-export-sidebar .outline-content { position: fixed; top: 0px; max-height: 100%; overflow: hidden auto; padding-bottom: 30px; padding-top: 60px; width: 300px; }
@media screen and (max-width: 1024px) {
  .typora-export-sidebar, .typora-export-sidebar .outline-content { width: 240px; }
}
@media screen and (max-width: 800px) {
  .typora-export-sidebar { display: none; }
}
.outline-content li, .outline-content ul { margin-left: 0px; margin-right: 0px; padding-left: 0px; padding-right: 0px; list-style: none; overflow-wrap: anywhere; }
.outline-content ul { margin-top: 0px; margin-bottom: 0px; }
.outline-content strong { font-weight: 400; }
.outline-expander { width: 1rem; height: 1.42857rem; position: relative; display: table-cell; vertical-align: middle; cursor: pointer; padding-left: 4px; }
.outline-expander::before { content: ""; position: relative; font-family: Ionicons; display: inline-block; font-size: 8px; vertical-align: middle; }
.outline-item { padding-top: 3px; padding-bottom: 3px; cursor: pointer; }
.outline-expander:hover::before { content: ""; }
.outline-h1 > .outline-item { padding-left: 0px; }
.outline-h2 > .outline-item { padding-left: 1em; }
.outline-h3 > .outline-item { padding-left: 2em; }
.outline-h4 > .outline-item { padding-left: 3em; }
.outline-h5 > .outline-item { padding-left: 4em; }
.outline-h6 > .outline-item { padding-left: 5em; }
.outline-label { cursor: pointer; display: table-cell; vertical-align: middle; text-decoration: none; color: inherit; }
.outline-label:hover { text-decoration: underline; }
.outline-item:hover { border-color: rgb(245, 245, 245); background-color: var(--item-hover-bg-color); }
.outline-item:hover { margin-left: -28px; margin-right: -28px; border-left: 28px solid transparent; border-right: 28px solid transparent; }
.outline-item-single .outline-expander::before, .outline-item-single .outline-expander:hover::before { display: none; }
.outline-item-open > .outline-item > .outline-expander::before { content: ""; }
.outline-children { display: none; }
.info-panel-tab-wrapper { display: none; }
.outline-item-open > .outline-children { display: block; }
.typora-export .outline-item { padding-top: 1px; padding-bottom: 1px; }
.typora-export .outline-item:hover { margin-right: -8px; border-right: 8px solid transparent; }
.typora-export .outline-expander::before { content: "+"; font-family: inherit; top: -1px; }
.typora-export .outline-expander:hover::before, .typora-export .outline-item-open > .outline-item > .outline-expander::before { content: "−"; }
.typora-export-collapse-outline .outline-children { display: none; }
.typora-export-collapse-outline .outline-item-open > .outline-children, .typora-export-no-collapse-outline .outline-children { display: block; }
.typora-export-no-collapse-outline .outline-expander::before { content: "" !important; }
.typora-export-show-outline .outline-item-active > .outline-item .outline-label { font-weight: 700; }
.md-inline-math-container mjx-container { zoom: 0.95; }
mjx-container { break-inside: avoid; }


/* meyer reset -- http://meyerweb.com/eric/tools/css/reset/ , v2.0 | 20110126 | License: none (public domain) */

@include-when-export url(https://fonts.googleapis.com/css?family=PT+Serif:400,400italic,700,700italic&subset=latin,cyrillic-ext,cyrillic,latin-ext);

/* =========== */

/* pt-serif-regular - latin */
/* pt-serif-italic - latin */
/* pt-serif-700 - latin */
/* pt-serif-700italic - latin */
:root {
    --active-file-bg-color: #dadada;
    --active-file-bg-color: rgba(32, 43, 51, 0.63);
    --active-file-text-color: white;
    --bg-color: #f3f2ee;
    --text-color: #1f0909;
    --control-text-color: #444;
    --rawblock-edit-panel-bd: #e5e5e5;

​    --select-text-bg-color: rgba(32, 43, 51, 0.63);
  --select-text-font-color: white;
}

pre {
    --select-text-bg-color: #36284e;
    --select-text-font-color: #fff;
}

html {
    font-size: 16px;
    -webkit-font-smoothing: antialiased;
}

html, body {
    background-color: #f3f2ee;
    font-family: "PT Serif", 'Times New Roman', Times, serif;
    color: #1f0909;
    line-height: 1.5em;
}

/*#write {
    overflow-x: auto;
    max-width: initial;
    padding-left: calc(50% - 17em);
    padding-right: calc(50% - 17em);
}

@media (max-width: 36em) {
    #write {
        padding-left: 1em;
        padding-right: 1em;
    }
}*/

#write {
    max-width: 40em;
}

@media only screen and (min-width: 1400px) {
    #write {
            max-width: 914px;
    }
}

ol li {
    list-style-type: decimal;
    list-style-position: outside;
}
ul li {
    list-style-type: disc;
    list-style-position: outside;
}

ol,
ul {
    list-style: none;
}

blockquote,
q {
    quotes: none;
}
blockquote:before,
blockquote:after,
q:before,
q:after {
    content: '';
    content: none;
}
table {
    border-collapse: collapse;
    border-spacing: 0;
}
/* styles */

/* ====== */

/* headings */

h1,
h2,
h3,
h4,
h5,
h6 {
    font-weight: bold;
}
h1 {
    font-size: 1.875em;
    /*30 / 16*/
    line-height: 1.6em;
    /* 48 / 30*/
    margin-top: 2em;
}
h2,
h3 {
    font-size: 1.3125em;
    /*21 / 16*/
    line-height: 1.15;
    /*24 / 21*/
    margin-top: 2.285714em;
    /*48 / 21*/
    margin-bottom: 1.15em;
    /*24 / 21*/
}
h3 {
    font-weight: normal;
}
h4 {
    font-size: 1.125em;
    /*18 / 16*/
    margin-top: 2.67em;
    /*48 / 18*/
}
h5,
h6 {
    font-size: 1em;
    /*16*/
}
h1 {
    border-bottom: 1px solid;
    margin-bottom: 1.875em;
    padding-bottom: 0.8125em;
}
/* links */

a {
    text-decoration: none;
    color: #065588;
}
a:hover,
a:active {
    text-decoration: underline;
}
/* block spacing */

p,
blockquote,
.md-fences {
    margin-bottom: 1.5em;
}
h1,
h2,
h3,
h4,
h5,
h6 {
    margin-bottom: 1.5em;
}
/* blockquote */

blockquote {
    font-style: italic;
    border-left: 5px solid;
    margin-left: 2em;
    padding-left: 1em;
}
/* lists */

ul,
ol {
    margin: 0 0 1.5em 1.5em;
}
/* tables */
.md-meta,.md-before, .md-after {
    color:#999;
}

table {
    margin-bottom: 1.5em;
    /*24 / 16*/
    font-size: 1em;
    /* width: 100%; */
}
thead th,
tfoot th {
    padding: .25em .25em .25em .4em;
    text-transform: uppercase;
}
th {
    text-align: left;
}
td {
    vertical-align: top;
    padding: .25em .25em .25em .4em;
}

code,
.md-fences {
    background-color: #dadada;
}

code {
    padding-left: 2px;
    padding-right: 2px;
}

.md-fences {
    margin-left: 2em;
    margin-bottom: 3em;
    padding-left: 1ch;
    padding-right: 1ch;
}

pre,
code,
tt {
    font-size: .875em;
    line-height: 1.714285em;
}
/* some fixes */

h1 {
    line-height: 1.3em;
    font-weight: normal;
    margin-bottom: 0.5em;
}

p + ul,
p + ol{
    margin-top: .5em;
}

h3 + ul,
h4 + ul,
h5 + ul,
h6 + ul,
h3 + ol,
h4 + ol,
h5 + ol,
h6 + ol {
    margin-top: .5em;
}

li > ul,
li > ol {
    margin-top: inherit;
    margin-bottom: 0;
}

li ol>li {
    list-style-type: lower-alpha;
}

li li ol>li{
    list-style-type: lower-roman;
}

h2,
h3 {
    margin-bottom: .75em;
}
hr {
    border-top: none;
    border-right: none;
    border-bottom: 1px solid;
    border-left: none;
}
h1 {
    border-color: #c5c5c5;
}
blockquote {
    border-color: #bababa;
    color: #656565;
}

blockquote ul,
blockquote ol {
    margin-left:0;
}

.ty-table-edit {
    background-color: transparent;
}
thead {
    background-color: #dadada;
}
tr:nth-child(even) {
    background: #e8e7e7;
}
hr {
    border-color: #c5c5c5;
}
.task-list{
    padding-left: 1rem;
}

.md-task-list-item {
    padding-left: 1.5rem;
    list-style-type: none;
}

.md-task-list-item > input:before {
    content: '\221A';
    display: inline-block;
    width: 1.25rem;
    height: 1.6rem;
    vertical-align: middle;
    text-align: center;
    color: #ddd;
    background-color: #F3F2EE;
}

.md-task-list-item > input:checked:before,
.md-task-list-item > input[checked]:before{
    color: inherit;
}

#write pre.md-meta-block {
    min-height: 1.875rem;
    color: #555;
    border: 0px;
    background: transparent;
    margin-top: -4px;
    margin-left: 1em;
    margin-top: 1em;
}

.md-image>.md-meta {
    color: #9B5146;
}

.md-image>.md-meta{
    font-family: Menlo, 'Ubuntu Mono', Consolas, 'Courier New', 'Microsoft Yahei', 'Hiragino Sans GB', 'WenQuanYi Micro Hei', serif;
}


#write>h3.md-focus:before{
    left: -1.5rem;
    color:#999;
    border-color:#999;
}
#write>h4.md-focus:before{
    left: -1.5rem;
    top: .25rem;
    color:#999;
    border-color:#999;
}
#write>h5.md-focus:before{
    left: -1.5rem;
    top: .0.3125rem;
    color:#999;
    border-color:#999;
}
#write>h6.md-focus:before{
    left: -1.5rem;
    top: 0.3125rem;
    color:#999;
    border-color:#999;
}

.md-toc:focus .md-toc-content{
    margin-top: 19px;
}

.md-toc-content:empty:before{
    color: #065588;
}
.md-toc-item {
    color: #065588;
}
#write div.md-toc-tooltip {
    background-color: #f3f2ee;
}

#typora-sidebar {
    background-color: #f3f2ee;
    -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, 0.375);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.375);
}

.pin-outline #typora-sidebar {
    background: inherit;
    box-shadow: none;
    border-right: 1px dashed;
}

.pin-outline #typora-sidebar:hover .outline-title-wrapper {
    border-left:1px dashed;
}

.outline-item:hover {
  background-color: #dadada;
  border-left: 28px solid #dadada;
  border-right: 18px solid #dadada;
}

.typora-node .outline-item:hover {
    border-right: 28px solid #dadada;
}

.outline-expander:before {
  content: "\f0da";
  font-family: FontAwesome;
  font-size:14px;
  top: 1px;
}

.outline-expander:hover:before,
.outline-item-open>.outline-item>.outline-expander:before {
  content: "\f0d7";
}

.modal-content {
    background-color: #f3f2ee;
}

.auto-suggest-container ul li {
    list-style-type: none;
}

/** UI for electron */

.megamenu-menu,
#top-titlebar, #top-titlebar *,
.megamenu-content {
    background: #f3f2ee;
    color: #1f0909;
}

.megamenu-menu-header {
    border-bottom: 1px dashed #202B33;
}

.megamenu-menu {
    box-shadow: none;
    border-right: 1px dashed;
}

header, .context-menu, .megamenu-content, footer {
    font-family: "PT Serif", 'Times New Roman', Times, serif;
    color: #1f0909;
}

#megamenu-back-btn {
    color: #1f0909;
    border-color: #1f0909;
}

.megamenu-menu-header #megamenu-menu-header-title:before {
    color: #1f0909;
}

.megamenu-menu-list li a:hover, .megamenu-menu-list li a.active {
    color: inherit;
    background-color: #e8e7df;
}

.long-btn:hover {
    background-color: #e8e7df;
}

#recent-file-panel tbody tr:nth-child(2n-1) {
    background-color: transparent !important;
}

.megamenu-menu-panel tbody tr:hover td:nth-child(2) {
    color: inherit;
}

.megamenu-menu-panel .btn {
    background-color: #D2D1D1;
}

.btn-default {
    background-color: transparent;
}

.typora-sourceview-on #toggle-sourceview-btn,
.ty-show-word-count #footer-word-count {
    background: #c7c5c5;
}

#typora-quick-open {
    background-color: inherit;
}

.md-diagram-panel {
    margin-top: 8px;
}

.file-list-item-file-name {
    font-weight: initial;
}

.file-list-item-summary {
    opacity: 1;
}

.file-list-item {
    color: #777;
}

.file-list-item.active {
    background-color: inherit;
    color: black;
}

.ty-side-sort-btn.active {
    background-color: inherit;
}

.file-list-item.active .file-list-item-file-name  {
    font-weight: bold;
}

.file-list-item{
    opacity:1 !important;
}

.file-library-node.active>.file-node-background{
    background-color: rgba(32, 43, 51, 0.63);
    background-color: var(--active-file-bg-color);
}

.file-tree-node.active>.file-node-content{
    color: white;
    color: var(--active-file-text-color);
}

.md-task-list-item>input {
    margin-left: -1.7em;
    margin-top: calc(1rem - 12px);
    -webkit-appearance: button;
}

input {
    border: 1px solid #aaa;
}

.megamenu-menu-header #megamenu-menu-header-title,
.megamenu-menu-header:hover, 
.megamenu-menu-header:focus {
    color: inherit;
}

.dropdown-menu .divider {
    border-color: #e5e5e5;
    opacity: 1;
}

/* https://github.com/typora/typora-issues/issues/2046 */
.os-windows-7 strong,
.os-windows-7 strong  {
    font-weight: 760;
}

.ty-preferences .btn-default {
    background: transparent;
}

.ty-preferences .window-header {
    border-bottom: 1px dashed #202B33;
    box-shadow: none;
}

#sidebar-loading-template, #sidebar-loading-template.file-list-item {
    color: #777;
}

.searchpanel-search-option-btn.active {
    background: #777;
    color: white;
}

.export-detail, .light .export-detail, 
.light .export-item.active, 
.light .export-items-list-control {
    background: #e0e0e0;
    border-radius: 2px;
    font-weight: 700;
    color: inherit
}


</style><title>Network UDP</title>
</head>
<body class='typora-export os-windows'><div class='typora-export-content'>
<div id='write'  class=''><p><span>UDP·UDP：User Datagram Protocol 用户数据报协议</span></p><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715515510753-fb158245-d308-4e29-879e-ec6fb6a929c3.png" referrerpolicy="no-referrer" alt="img"></p><p>&nbsp;</p><h1><span>一、UDP 基础</span></h1><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1723126387867-fddba04f-b181-4327-bb33-770f12460c78.png" alt="img" style="zoom: 67%;" /></p><p>&nbsp;</p><p><span>如果数据部分和 EDC 部分都出错，并且错误刚好对上叫做残存错误。</span></p><p><span>给发送方做差速控制编码。在传送过程中出了一个 bit 的错误都能检测到。</span></p><p><span>UDP 被用于：</span></p><ul><li><p><span>流媒体</span></p></li><li><p><span>DNS</span></p></li></ul><p>&nbsp;</p><p>&nbsp;</p><h1 id='二rdt-可靠数据传输'><span>二、RDT 可靠数据传输</span></h1><h2 id='一-问题描述'><span>(一) 问题描述</span></h2><h3 id='1-rdt-简述'><span>1. Rdt 简述</span></h3><p><span>Rdt 在应用层、传输层和数据链路层都很重要。</span></p><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715740432937-d90c4efe-c926-43ab-8912-3240eefdafc1.png?x-oss-process=image%2Fformat%2Cwebp%2Fresize%2Cw_937%2Climit_0" alt="image.png" style="zoom:50%;" /></p><p><span>packet是抽象的形成本层的数据协议单元，实际上在 tcp 中封装为 segment。</span></p><p><span>Rdt 面临的问题就是，即要向上层提供可靠的服务，但是依赖的服务又不可靠。</span></p><h3 id='2-有限状态机'><span>2. 有限状态机</span></h3><p><span>我们接下来将使用有限状态机描述状态变迁。</span></p><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1716097123636-074dba50-8f9c-49e5-a4d4-f636fa67710f.png?x-oss-process=image%2Fformat%2Cwebp" alt="image.png" style="zoom:50%;" /></p><p><span>使用有限状态机（FSM）来描述发送方和接收方。状态变迁 edge 把两个状态连接在一起。</span></p><p><span>在变迁的这条边上有标注，有分子和分母。</span></p><ul><li><p><span>分子代表这个状态有什么事情发生，有这个事情发生，要从这个状态变迁到这个状态。</span></p></li><li><p><span>分母描述了变迁状态时，协议需要做的动作。</span></p></li></ul><p>&nbsp;</p><h2 id='二-rdt-完善之路'><span>(二) Rdt 完善之路</span></h2><h3 id='1-rdt-10可靠信道的可靠数据传输'><span>1. Rdt 1.0：可靠信道的可靠数据传输</span></h3><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715742467881-98be64d5-423d-4fb1-995f-d001f73a0e00.png?x-oss-process=image%2Fformat%2Cwebp" alt="image.png" style="zoom:50%;" /></p><p><span>Rdt 发送端只通过 </span><code>rdt_send(data)</code><span>事件接受来自较高层的数据，产生一个包含该数据的分组。</span></p><p><span>（经由 </span><code>make_pkt(data)</code><span>操作），并将分组发送到信道中。实际上，</span><code>rdt_send(data）</code><span>事件是由较高层应用的过程调用产生的（例如，rdt_send())。</span></p><p><span>在接受端，rdt 通过 </span><code>rdt_rcv(packet)</code><span>事·件从底层信道接受分组，提取数据后将数据上传较高层。实际上 </span><code>rdt_rcv(packet)</code><span>  事件是由较低层协议的过程调用产生的。</span></p><h3 id='2-rdt-20具有比特差错信道的可靠数据传输'><span>2. Rdt 2.0：具有比特差错信道的可靠数据传输</span></h3><p><span>如果分组中的比特出现差错会进行重传。基于重传机制的数据传输协议称为</span><strong><span>自动重传请求</span></strong><span> （Automatic Repeat reQuest， ARQ）协议。</span></p><p><span>ARQ 协议需要另外三种协议功能来处理比特差错情况：</span></p><ul><li><p><span>差错检测。</span></p></li><li><p><span>接收方反馈。</span></p></li><li><p><span>重传。</span></p></li></ul><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715745179642-38f08b9d-8f3b-45ad-bc7d-0c9396d09795.png?x-oss-process=image%2Fformat%2Cwebp" alt="image.png" style="zoom: 50%;" /></p><p><span>rdt 2.0 协议存在致命缺陷，没有考虑 ACK 或 NAK 分组受损的可能性。</span></p><p>&nbsp;</p><p><span>解决这个问题的方法时在数据分组中添加一个新字段，让发送方对其数据分组编号，即发送数据分组的</span><strong><span>序号</span></strong><span>放在该字段。于是，接收方只需要检查序号即可确定收到的分组是否为重传。</span></p><p><span>对于停等协议，1 个比特序号就足够，因为他可让接收方知道发送方是否正在重传前一个发送分组。</span></p><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715749883417-f8dc83e7-7596-4c04-ba42-6d75c4452924.png?x-oss-process=image%2Fformat%2Cwebp%2Fresize%2Cw_937%2Climit_0" alt="image.png" style="zoom:50%;" /></p><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715749854768-bf0142c0-bfbe-42ed-b2e7-55a901da8b62.png?x-oss-process=image%2Fformat%2Cwebp%2Fresize%2Cw_937%2Climit_0" alt="image.png" style="zoom:50%;" /></p><p><span>rdt 2.1 的发送方和接收方 FSM 状态数都是以前的两倍。</span></p><p><span>这是因为协议状态此时必须反应出目前正发送的分组或希望接收的分组的序号是 0 还是 1。</span></p><p>&nbsp;</p><p><span>因为发送 NAK 与对上次正确接受的分组发送一个 ACK 也能实现一样的效果。 所以 rdt 2.2 是在有比特差错信道上实现的一个无 NAK 的可靠数据传输协议。</span></p><p><img src="https://cdn.nlark.com/yuque/0/2024/jpeg/40540759/1715753548611-ec63a926-96fe-4e1b-a399-f7771d28b474.jpeg?x-oss-process=image%2Fformat%2Cwebp" alt="Wait+for+call+0+from+above.jpg" style="zoom:50%;" /></p><p><img src="https://cdn.nlark.com/yuque/0/2024/jpeg/40540759/1715753562503-283e4f4f-f582-4c67-be30-68da06481757.jpeg?x-oss-process=image%2Fformat%2Cwebp" alt="rdt2.2_+receiver+FSM+receiver+FSM.jpg" style="zoom:50%;" /></p><h3 id='3-rdt-30具有比特差错的丢包信道的可靠数据传输'><span>3. Rdt 3.0：具有比特差错的丢包信道的可靠数据传输</span></h3><p><span>我们已经假定完了比特受损，但是底层信道还会丢包。</span></p><p><span>分组丢失，路由器具有 queue 队列，来了分组 push 进队列，队列如果满了就是丢弃。</span></p><p>&nbsp;</p><p><span>为了解决这个问题，rdt 加入了新的机制，超时重传机制。为了实现基于事件的重传机制，需要一个</span><strong><span>倒计数定时器</span></strong><span>，在一个给定的时间量过期后，可以中断发送方。因此，发送方要能做到：① 每发送一次分组，便启动一个定时器。② 响应定时器中断 ③ 终止定时器。</span></p><p><span>因为分组序号在 0，1 之间交替，rdt 3.0 又被称为</span><strong><span>比特交替协议</span></strong><span>（alternating-bit protocol)</span><strong><span>。</span></strong></p><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715766395328-ce0dbfb7-3ebb-4c26-8524-30ac4d89b303.png?x-oss-process=image%2Fformat%2Cwebp%2Fresize%2Cw_937%2Climit_0" alt="屏幕截图 2024-05-15 144319.png" style="zoom: 67%;" /></p><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715766449733-fe1250da-49dd-49f4-8d40-a8add6f6e08c.png?x-oss-process=image%2Fformat%2Cwebp" alt="image.png" style="zoom:50%;" /></p><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715766473880-1025e488-1af9-46dc-8189-5f2e1fb0bf4f.png?x-oss-process=image%2Fcrop%2Cx_11%2Cy_0%2Cw_1057%2Ch_694" alt="img" style="zoom:67%;" /></p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><h2 id='三-流水线可靠数据传输协议'><span>(三) 流水线可靠数据传输协议</span></h2><p><span>  Rdt 性能问题的核心在于它是一个停等协议。 链路容量比较大，一次发一个PDU 的不能够充分利用链路的传输能力  。所以我们提出了</span><strong><span>流水线，</span></strong><span>不以停等方式运行，允许发送方发送多个分组而无需等待确认。为了实现流水线技术，可靠数据传输协议做以下升级：</span></p><ul><li><p><span>增加序号范围，因为每个输送中的分组必须有一个唯一的序号，而且可能有多个输送中未确认的报文。</span></p></li><li><p><span>协议的发送方、接收方两端缓存多个分组。发送方缓存已发送但是未确认的分组，接收方或许需要缓存已经正确确认的分组。</span></p></li><li><p><span>序号范围和对缓冲的要求取决于数据传输协议如何处理丢失、损坏以及延时过大。解决这两个差错的两种方法：</span><strong><span>回退 N 步</span></strong><span> 和 </span><strong><span>选择重传。</span></strong></p></li></ul><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715769651599-a7da2289-e91b-4160-b00d-a87916a148e4.png?x-oss-process=image%2Fformat%2Cwebp" referrerpolicy="no-referrer" alt="image.png"></p><h3 id='1-回退-n-步'><span>1. 回退 N 步</span></h3><p><span>在</span><strong><span>回退 N 步</span></strong><span> 协议，允许发送方发送多个分组而不需等待确认。</span></p><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715837072834-5464221c-7dd8-4549-920b-fec5cf5df371.png?x-oss-process=image%2Fformat%2Cwebp" referrerpolicy="no-referrer" alt="image.png"></p><p><span>将 </span><strong><span>send_base</span></strong><span> 定义为最早未确认分组的序号，将 </span><strong><span>nextseqnum</span></strong><span> 定义为最小的未使用序号。</span></p><p><span>那些已被发送但还未被确认的分组的许可序号范围可以被看成是一个在序号范围内长度为 N 的窗口。随着协议的运行，该窗口在序号空间向前滑动。N 因此被称为</span><strong><span>窗口长度</span></strong><span>，GBN 也被称为</span><strong><span>滑动窗口协议</span></strong><span>。</span></p><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715839173172-96deb33b-8a5f-498b-9792-8b61b3c7549e.png?x-oss-process=image%2Fformat%2Cwebp%2Fresize%2Cw_937%2Climit_0" referrerpolicy="no-referrer" alt="img"></p><p>&nbsp;</p><p><span>GBN 发送方必须响应三种类型的事件：</span></p><ul><li><p><strong><span>上层的调用。</span></strong><span>当上层调用 send()的时候，发送方首先检查发送窗口是否已满，即是否已有 N 个已发送但是未被确认的分组。</span></p></li></ul><p><span>  未满，产生分组将其发送，更新相应变量。窗口已满，发送方数据返回上层，隐式提醒上层窗口已满，待会儿再试。</span></p><p><span>实际中，发送方会可能缓存这些数据，或使用同步机制允许上层仅在窗口不满的时候调用 send()。</span></p><ul><li><p><strong><span>收到 ACK。</span></strong><span>在 GBN 协议中，对序号为 n 的分组确认采取</span><strong><span>累计确认</span></strong><span>方式，表明已经正确接收序号为 n 以及 n 以前的所有分组。。 </span></p></li><li><p><strong><span>超时事件。</span></strong><span>使用定时器用于恢复数据或确认分组丢失。发送方使用一个定时器，它可被当作最早的已发送但未被确认的分组所使用的定时器。</span></p></li></ul><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715841815940-d8bf8979-16d8-438e-ae79-fae95a2463cd.png?x-oss-process=image%2Fformat%2Cwebp" referrerpolicy="no-referrer" alt="image.png"></p><p><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715842247043-7e6adac9-cb1a-4871-ab44-70b6761ebdc2.png?x-oss-process=image%2Fformat%2Cwebp" referrerpolicy="no-referrer" alt="image.png"></p><p><span>  </span><strong><span>在 GBN 接收方中，序号为 n 的分组被正确接收，且按序（上一个交付给上层的数据是序号 n-1 的分组），则为分组 n 发送一个 ACK，并将数据交付上层。其他所有情况，丢弃分组。</span></strong></p><p><span>  这种方法看起来有些愚蠢。如果期望的 n，先到了 n+1，其实也可以将序号为 n+1 的分组缓存，交付完成 序号为 n 的分组后，再交付序号为 n+1 的分组。</span></p><p><span>  这种简单丢弃的方法优点就是不用缓存任何失序分组，接收方只需要维护 expectedseqnum 变量的更新即可。</span></p><p>&nbsp;</p><h3 id='2-选择重传'><span>2. 选择重传</span></h3><p><span>在 GBN 中单个分组的差错引起 GBN 重传大量分组，许多分组没有重传的必要。选择重传协议通过让发送方仅重传那些他怀疑在接收方出错的分组而避免了不必要的重传。</span></p><p><span> </span><img src="https://cdn.nlark.com/yuque/0/2024/png/40540759/1715863220224-edacf192-300e-4c10-acac-c1e63c3c2b1d.png?x-oss-process=image%2Fformat%2Cwebp" referrerpolicy="no-referrer" alt="image.png"></p><p><span>SR 接收方将确认一个正确接收的分组而不管其是否按序。失序的分组被缓存直到所有丢失分组（即序号更小的分组）都被收到为止，这时才可以将一批分组按序交付给上层。</span></p><hr /><figure class='table-figure'><table><thead><tr><th style='text-align:left;' ><span> SR Sender</span></th><th style='text-align:left;' ><span>SR Sende</span></th></tr></thead><tbody><tr><td style='text-align:left;' ><span>1.</span><strong><span>从上层收到数据</span></strong><span>。当从上层接收到数据，SR发送方检查下一个可用于该分组的序号。如果序号位于发送方的窗口内，将数据打包发送；否则仍旧像GBN中一样，要么缓存数据，要么返回给上层以便以后传输。</span></td><td style='text-align:left;' ><span>1.</span><strong><span>序号在[rcv_base,rcv_base+N-1]内的分组被正确接收。</span></strong><span>返回一个ACK，如果该分组没收到过则缓存。如果分组序号等于接收窗口的基序号，则该分组以及以前缓存的序号连续的分组交付给上层。然后，接收窗口向前移动分组的编号向上交付这些分组</span></td></tr><tr><td style='text-align:left;' ><span>2.</span><strong><span>超时。</span></strong><span>定时器被用来防止丢失分组，但是与GBN不同的是，每个分组都必须拥有自己的逻辑定时器。</span></td><td style='text-align:left;' ><span>2.</span><strong><span>序号在[rcv_base-N,rcv_base-1]内的分组被正确接收。</span></strong><span>此时产生一个ACK，即使该分组是接受方以前已确认的分组。</span></td></tr><tr><td style='text-align:left;' ><span>3.</span><strong><span>收到ACK。</span></strong><span>如果收到ACK，倘若该分组在窗口内，则SR发送方将那个被确认的分组标记为已被接收。如果该分组的序号等于send_base,则窗口基序号向前移动到具有最小序号的未确认分组处。窗口移动，有序号落在窗口内，发送这些分组</span></td><td style='text-align:left;' ><span>3.</span><strong><span>其他情况。</span></strong><span>忽略</span></td></tr></tbody></table></figure><p>&nbsp;</p></div></div>
</body>
</html>

{% endraw %}
