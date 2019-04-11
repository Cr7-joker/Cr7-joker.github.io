---
title: How to use Typora
tags: Blog Markdown
edit: 2019-01-28T00:00:00.000Z
categories: Blog
status: Completed
description: >-
  Typora is the ultimate compact markdown editor that supports the editing of
  mathematical formulas, can be exported to pdf and HTML, etc. I will briefly
  describe the basic usage of typora.
---

<html>
<head>
<meta charset='UTF-8'><meta name='viewport' content='width=device-width initial-scale=1'>
<title>How to use Typora</title><link href='https://fonts.loli.net/css?family=Open+Sans:400italic,700italic,700,400&subset=latin,latin-ext' rel='stylesheet' type='text/css' /><style type='text/css'>html {overflow-x: initial !important;}:root { --bg-color:#ffffff; --text-color:#333333; --select-text-bg-color:#B5D6FC; --select-text-font-color:auto; --monospace:"Lucida Console",Consolas,"Courier",monospace; }
html { font-size: 14px; background-color: var(--bg-color); color: var(--text-color); font-family: "Helvetica Neue", Helvetica, Arial, sans-serif; -webkit-font-smoothing: antialiased; }
body { margin: 0px; padding: 0px; height: auto; bottom: 0px; top: 0px; left: 0px; right: 0px; font-size: 1rem; line-height: 1.42857; overflow-x: hidden; background: inherit; }
iframe { margin: auto; }
a.url { word-break: break-all; }
a:active, a:hover { outline: 0px; }
.in-text-selection, ::selection { text-shadow: none; background: var(--select-text-bg-color); color: var(--select-text-font-color); }
#write { margin: 0px auto; height: auto; width: inherit; word-break: normal; word-wrap: break-word; position: relative; white-space: normal; overflow-x: visible; padding-top: 40px; }
#write.first-line-indent p { text-indent: 2em; }
#write.first-line-indent li p, #write.first-line-indent p * { text-indent: 0px; }
#write.first-line-indent li { margin-left: 2em; }
.for-image #write { padding-left: 8px; padding-right: 8px; }
body.typora-export { padding-left: 30px; padding-right: 30px; }
.typora-export .footnote-line, .typora-export li, .typora-export p { white-space: pre-wrap; }
@media screen and (max-width: 500px) {
  body.typora-export { padding-left: 0px; padding-right: 0px; }
  .CodeMirror-sizer { margin-left: 0px !important; }
  .CodeMirror-gutters { display: none !important; }
}
#write li > figure:first-child { margin-top: -20px; }
#write ol, #write ul { position: relative; }
img { max-width: 100%; vertical-align: middle; }
button, input, select, textarea { color: inherit; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; font-size: inherit; line-height: inherit; font-family: inherit; }
input[type="checkbox"], input[type="radio"] { line-height: normal; padding: 0px; }
*, ::after, ::before { box-sizing: border-box; }
#write h1, #write h2, #write h3, #write h4, #write h5, #write h6, #write p, #write pre { width: inherit; }
#write h1, #write h2, #write h3, #write h4, #write h5, #write h6, #write p { position: relative; }
h1, h2, h3, h4, h5, h6 { break-after: avoid-page; break-inside: avoid; orphans: 2; }
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
figure > table { margin: 0px !important; }
tr { break-inside: avoid; break-after: auto; }
thead { display: table-header-group; }
table { border-collapse: collapse; border-spacing: 0px; width: 100%; overflow: auto; break-inside: auto; text-align: left; }
table.md-table td { min-width: 32px; }
.CodeMirror-gutters { border-right: 0px; background-color: inherit; }
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
.md-diagram-panel { width: 100%; margin-top: 10px; text-align: center; padding-top: 0px; padding-bottom: 8px; overflow-x: auto; }
#write .md-fences.mock-cm { white-space: pre-wrap; }
.md-fences.md-fences-with-lineno { padding-left: 0px; }
#write.fences-no-line-wrapping .md-fences.mock-cm { white-space: pre; overflow-x: auto; }
.md-fences.mock-cm.md-fences-with-lineno { padding-left: 8px; }
.CodeMirror-line, twitterwidget { break-inside: avoid; }
.footnotes { opacity: 0.8; font-size: 0.9rem; margin-top: 1em; margin-bottom: 1em; }
.footnotes + .footnotes { margin-top: 0px; }
.md-reset { margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: top; background: 0px 0px; text-decoration: none; text-shadow: none; float: none; position: static; width: auto; height: auto; white-space: nowrap; cursor: inherit; -webkit-tap-highlight-color: transparent; line-height: normal; font-weight: 400; text-align: left; box-sizing: content-box; direction: ltr; }
li div { padding-top: 0px; }
blockquote { margin: 1rem 0px; }
li .mathjax-block, li p { margin: 0.5rem 0px; }
li { margin: 0px; position: relative; }
blockquote > :last-child { margin-bottom: 0px; }
blockquote > :first-child, li > :first-child { margin-top: 0px; }
.footnotes-area { color: rgb(136, 136, 136); margin-top: 0.714rem; padding-bottom: 0.143rem; white-space: normal; }
#write .footnote-line { white-space: pre-wrap; }
@media print {
  body, html { border: 1px solid transparent; height: 99%; break-after: avoid; break-before: avoid; }
  #write { margin-top: 0px; padding-top: 0px; border-color: transparent !important; }
  .typora-export * { -webkit-print-color-adjust: exact; }
  html.blink-to-pdf { font-size: 13px; }
  .typora-export #write { padding-left: 32px; padding-right: 32px; padding-bottom: 0px; break-after: avoid; }
  .typora-export #write::after { height: 0px; }
  @page { margin: 20mm 0px; }
}
.footnote-line { margin-top: 0.714em; font-size: 0.7em; }
a img, img a { cursor: pointer; }
pre.md-meta-block { font-size: 0.8rem; min-height: 0.8rem; white-space: pre-wrap; background: rgb(204, 204, 204); display: block; overflow-x: hidden; }
p > .md-image:only-child:not(.md-img-error) img, p > img:only-child { display: block; margin: auto; }
p > .md-image:only-child { display: inline-block; width: 100%; }
#write .MathJax_Display { margin: 0.8em 0px 0px; }
.md-math-block { width: 100%; }
.md-math-block:not(:empty)::after { display: none; }
[contenteditable="true"]:active, [contenteditable="true"]:focus { outline: 0px; box-shadow: none; }
.md-task-list-item { position: relative; list-style-type: none; }
.task-list-item.md-task-list-item { padding-left: 0px; }
.md-task-list-item > input { position: absolute; top: 0px; left: 0px; margin-left: -1.2em; margin-top: calc(1em - 10px); }
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
.md-attr { display: none; }
.md-fn-count::after { content: "."; }
code, pre, samp, tt { font-family: var(--monospace); }
kbd { margin: 0px 0.1em; padding: 0.1em 0.6em; font-size: 0.8em; color: rgb(36, 39, 41); background: rgb(255, 255, 255); border: 1px solid rgb(173, 179, 185); border-radius: 3px; box-shadow: rgba(12, 13, 14, 0.2) 0px 1px 0px, rgb(255, 255, 255) 0px 0px 0px 2px inset; white-space: nowrap; vertical-align: middle; }
.md-comment { color: rgb(162, 127, 3); opacity: 0.8; font-family: var(--monospace); }
code { text-align: left; vertical-align: initial; }
a.md-print-anchor { white-space: pre !important; border-width: initial !important; border-style: none !important; border-color: initial !important; display: inline-block !important; position: absolute !important; width: 1px !important; right: 0px !important; outline: 0px !important; background: 0px 0px !important; text-decoration: initial !important; text-shadow: initial !important; }
.md-inline-math .MathJax_SVG .noError { display: none !important; }
.html-for-mac .inline-math-svg .MathJax_SVG { vertical-align: 0.2px; }
.md-math-block .MathJax_SVG_Display { text-align: center; margin: 0px; position: relative; text-indent: 0px; max-width: none; max-height: none; min-height: 0px; min-width: 100%; width: auto; overflow-y: hidden; display: block !important; }
.MathJax_SVG_Display, .md-inline-math .MathJax_SVG_Display { width: auto; margin: inherit; display: inline-block !important; }
.MathJax_SVG .MJX-monospace { font-family: var(--monospace); }
.MathJax_SVG .MJX-sans-serif { font-family: sans-serif; }
.MathJax_SVG { display: inline; font-style: normal; font-weight: 400; line-height: normal; zoom: 90%; text-indent: 0px; text-align: left; text-transform: none; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; direction: ltr; max-width: none; max-height: none; min-width: 0px; min-height: 0px; border: 0px; padding: 0px; margin: 0px; }
.MathJax_SVG * { transition: none; }
.MathJax_SVG_Display svg { vertical-align: middle !important; margin-bottom: 0px !important; }
.os-windows.monocolor-emoji .md-emoji { font-family: "Segoe UI Symbol", sans-serif; }
.md-diagram-panel > svg { max-width: 100%; }
[lang="mermaid"] svg, [lang="flow"] svg { max-width: 100%; }
[lang="mermaid"] .node text { font-size: 1rem; }
table tr th { border-bottom: 0px; }
video { max-width: 100%; display: block; margin: 0px auto; }
iframe { max-width: 100%; width: 100%; border: none; }
.highlight td, .highlight tr { border: 0px; }


.CodeMirror { height: auto; }
.CodeMirror.cm-s-inner { background: inherit; }
.CodeMirror-scroll { overflow-y: hidden; overflow-x: auto; z-index: 3; }
.CodeMirror-gutter-filler, .CodeMirror-scrollbar-filler { background-color: rgb(255, 255, 255); }
.CodeMirror-gutters { border-right: 1px solid rgb(221, 221, 221); background: inherit; white-space: nowrap; }
.CodeMirror-linenumber { padding: 0px 3px 0px 5px; text-align: right; color: rgb(153, 153, 153); }
.cm-s-inner .cm-keyword { color: rgb(119, 0, 136); }
.cm-s-inner .cm-atom, .cm-s-inner.cm-atom { color: rgb(34, 17, 153); }
.cm-s-inner .cm-number { color: rgb(17, 102, 68); }
.cm-s-inner .cm-def { color: rgb(0, 0, 255); }
.cm-s-inner .cm-variable { color: rgb(0, 0, 0); }
.cm-s-inner .cm-variable-2 { color: rgb(0, 85, 170); }
.cm-s-inner .cm-variable-3 { color: rgb(0, 136, 85); }
.cm-s-inner .cm-string { color: rgb(170, 17, 17); }
.cm-s-inner .cm-property { color: rgb(0, 0, 0); }
.cm-s-inner .cm-operator { color: rgb(152, 26, 26); }
.cm-s-inner .cm-comment, .cm-s-inner.cm-comment { color: rgb(170, 85, 0); }
.cm-s-inner .cm-string-2 { color: rgb(255, 85, 0); }
.cm-s-inner .cm-meta { color: rgb(85, 85, 85); }
.cm-s-inner .cm-qualifier { color: rgb(85, 85, 85); }
.cm-s-inner .cm-builtin { color: rgb(51, 0, 170); }
.cm-s-inner .cm-bracket { color: rgb(153, 153, 119); }
.cm-s-inner .cm-tag { color: rgb(17, 119, 0); }
.cm-s-inner .cm-attribute { color: rgb(0, 0, 204); }
.cm-s-inner .cm-header, .cm-s-inner.cm-header { color: rgb(0, 0, 255); }
.cm-s-inner .cm-quote, .cm-s-inner.cm-quote { color: rgb(0, 153, 0); }
.cm-s-inner .cm-hr, .cm-s-inner.cm-hr { color: rgb(153, 153, 153); }
.cm-s-inner .cm-link, .cm-s-inner.cm-link { color: rgb(0, 0, 204); }
.cm-negative { color: rgb(221, 68, 68); }
.cm-positive { color: rgb(34, 153, 34); }
.cm-header, .cm-strong { font-weight: 700; }
.cm-del { text-decoration: line-through; }
.cm-em { font-style: italic; }
.cm-link { text-decoration: underline; }
.cm-error { color: red; }
.cm-invalidchar { color: red; }
.cm-constant { color: rgb(38, 139, 210); }
.cm-defined { color: rgb(181, 137, 0); }
div.CodeMirror span.CodeMirror-matchingbracket { color: rgb(0, 255, 0); }
div.CodeMirror span.CodeMirror-nonmatchingbracket { color: rgb(255, 34, 34); }
.cm-s-inner .CodeMirror-activeline-background { background: inherit; }
.CodeMirror { position: relative; overflow: hidden; }
.CodeMirror-scroll { height: 100%; outline: 0px; position: relative; box-sizing: content-box; background: inherit; }
.CodeMirror-sizer { position: relative; }
.CodeMirror-gutter-filler, .CodeMirror-hscrollbar, .CodeMirror-scrollbar-filler, .CodeMirror-vscrollbar { position: absolute; z-index: 6; display: none; }
.CodeMirror-vscrollbar { right: 0px; top: 0px; overflow: hidden; }
.CodeMirror-hscrollbar { bottom: 0px; left: 0px; overflow: hidden; }
.CodeMirror-scrollbar-filler { right: 0px; bottom: 0px; }
.CodeMirror-gutter-filler { left: 0px; bottom: 0px; }
.CodeMirror-gutters { position: absolute; left: 0px; top: 0px; padding-bottom: 30px; z-index: 3; }
.CodeMirror-gutter { white-space: normal; height: 100%; box-sizing: content-box; padding-bottom: 30px; margin-bottom: -32px; display: inline-block; }
.CodeMirror-gutter-wrapper { position: absolute; z-index: 4; background: 0px 0px !important; border: none !important; }
.CodeMirror-gutter-background { position: absolute; top: 0px; bottom: 0px; z-index: 4; }
.CodeMirror-gutter-elt { position: absolute; cursor: default; z-index: 4; }
.CodeMirror-lines { cursor: text; }
.CodeMirror pre { border-radius: 0px; border-width: 0px; background: 0px 0px; font-family: inherit; font-size: inherit; margin: 0px; white-space: pre; word-wrap: normal; color: inherit; z-index: 2; position: relative; overflow: visible; }
.CodeMirror-wrap pre { word-wrap: break-word; white-space: pre-wrap; word-break: normal; }
.CodeMirror-code pre { border-right: 30px solid transparent; width: fit-content; }
.CodeMirror-wrap .CodeMirror-code pre { border-right: none; width: auto; }
.CodeMirror-linebackground { position: absolute; left: 0px; right: 0px; top: 0px; bottom: 0px; z-index: 0; }
.CodeMirror-linewidget { position: relative; z-index: 2; overflow: auto; }
.CodeMirror-wrap .CodeMirror-scroll { overflow-x: hidden; }
.CodeMirror-measure { position: absolute; width: 100%; height: 0px; overflow: hidden; visibility: hidden; }
.CodeMirror-measure pre { position: static; }
.CodeMirror div.CodeMirror-cursor { position: absolute; visibility: hidden; border-right: none; width: 0px; }
.CodeMirror div.CodeMirror-cursor { visibility: hidden; }
.CodeMirror-focused div.CodeMirror-cursor { visibility: inherit; }
.cm-searching { background: rgba(255, 255, 0, 0.4); }
@media print {
  .CodeMirror div.CodeMirror-cursor { visibility: hidden; }
}


:root { --side-bar-bg-color: #fafafa; --control-text-color: #777; }
html { font-size: 16px; }
body { font-family: "Open Sans", "Clear Sans", "Helvetica Neue", Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.6; }
#write { max-width: 860px; margin: 0px auto; padding: 30px 30px 100px; }
#write > ul:first-child, #write > ol:first-child { margin-top: 30px; }
a { color: rgb(65, 131, 196); }
h1, h2, h3, h4, h5, h6 { position: relative; margin-top: 1rem; margin-bottom: 1rem; font-weight: bold; line-height: 1.4; cursor: text; }
h1:hover a.anchor, h2:hover a.anchor, h3:hover a.anchor, h4:hover a.anchor, h5:hover a.anchor, h6:hover a.anchor { text-decoration: none; }
h1 tt, h1 code { font-size: inherit; }
h2 tt, h2 code { font-size: inherit; }
h3 tt, h3 code { font-size: inherit; }
h4 tt, h4 code { font-size: inherit; }
h5 tt, h5 code { font-size: inherit; }
h6 tt, h6 code { font-size: inherit; }
h1 { padding-bottom: 0.3em; font-size: 2.25em; line-height: 1.2; border-bottom: 1px solid rgb(238, 238, 238); }
h2 { padding-bottom: 0.3em; font-size: 1.75em; line-height: 1.225; border-bottom: 1px solid rgb(238, 238, 238); }
h3 { font-size: 1.5em; line-height: 1.43; }
h4 { font-size: 1.25em; }
h5 { font-size: 1em; }
h6 { font-size: 1em; color: rgb(119, 119, 119); }
p, blockquote, ul, ol, dl, table { margin: 0.8em 0px; }
li > ol, li > ul { margin: 0px; }
hr { height: 2px; padding: 0px; margin: 16px 0px; background-color: rgb(231, 231, 231); border: 0px none; overflow: hidden; box-sizing: content-box; }
li p.first { display: inline-block; }
ul, ol { padding-left: 30px; }
ul:first-child, ol:first-child { margin-top: 0px; }
ul:last-child, ol:last-child { margin-bottom: 0px; }
blockquote { border-left: 4px solid rgb(223, 226, 229); padding: 0px 15px; color: rgb(119, 119, 119); }
blockquote blockquote { padding-right: 0px; }
table { padding: 0px; word-break: initial; }
table tr { border-top: 1px solid rgb(223, 226, 229); margin: 0px; padding: 0px; }
table tr:nth-child(2n), thead { background-color: rgb(248, 248, 248); }
table tr th { font-weight: bold; border-width: 1px 1px 0px; border-top-style: solid; border-right-style: solid; border-left-style: solid; border-top-color: rgb(223, 226, 229); border-right-color: rgb(223, 226, 229); border-left-color: rgb(223, 226, 229); border-image: initial; border-bottom-style: initial; border-bottom-color: initial; text-align: left; margin: 0px; padding: 6px 13px; }
table tr td { border: 1px solid rgb(223, 226, 229); text-align: left; margin: 0px; padding: 6px 13px; }
table tr th:first-child, table tr td:first-child { margin-top: 0px; }
table tr th:last-child, table tr td:last-child { margin-bottom: 0px; }
.CodeMirror-lines { padding-left: 4px; }
.code-tooltip { box-shadow: rgba(0, 28, 36, 0.3) 0px 1px 1px 0px; border-top: 1px solid rgb(238, 242, 242); }
.md-fences, code, tt { border: 1px solid rgb(231, 234, 237); background-color: rgb(248, 248, 248); border-radius: 3px; padding: 2px 4px 0px; font-size: 0.9em; }
code { background-color: rgb(243, 244, 244); padding: 0px 2px; }
.md-fences { margin-bottom: 15px; margin-top: 15px; padding: 8px 1em 6px; }
.md-task-list-item > input { margin-left: -1.3em; }
@media print {
  html { font-size: 13px; }
  table, pre { break-inside: avoid; }
  pre { word-wrap: break-word; }
}
.md-fences { background-color: rgb(248, 248, 248); }
#write pre.md-meta-block { padding: 1rem; font-size: 85%; line-height: 1.45; background-color: rgb(247, 247, 247); border: 0px; border-radius: 3px; color: rgb(119, 119, 119); margin-top: 0px !important; }
.mathjax-block > .code-tooltip { bottom: 0.375rem; }
.md-mathjax-midline { background: rgb(250, 250, 250); }
#write > h3.md-focus::before { left: -1.5625rem; top: 0.375rem; }
#write > h4.md-focus::before { left: -1.5625rem; top: 0.285714rem; }
#write > h5.md-focus::before { left: -1.5625rem; top: 0.285714rem; }
#write > h6.md-focus::before { left: -1.5625rem; top: 0.285714rem; }
.md-image > .md-meta { border-radius: 3px; padding: 2px 0px 0px 4px; font-size: 0.9em; color: inherit; }
.md-tag { color: rgb(167, 167, 167); opacity: 1; }
.md-toc { margin-top: 20px; padding-bottom: 20px; }
.sidebar-tabs { border-bottom: none; }
#typora-quick-open { border: 1px solid rgb(221, 221, 221); background-color: rgb(248, 248, 248); }
#typora-quick-open-item { background-color: rgb(250, 250, 250); border-color: rgb(254, 254, 254) rgb(229, 229, 229) rgb(229, 229, 229) rgb(238, 238, 238); border-style: solid; border-width: 1px; }
.on-focus-mode blockquote { border-left-color: rgba(85, 85, 85, 0.12); }
header, .context-menu, .megamenu-content, footer { font-family: "Segoe UI", Arial, sans-serif; }
.file-node-content:hover .file-node-icon, .file-node-content:hover .file-node-open-state { visibility: visible; }
.mac-seamless-mode #typora-sidebar { background-color: var(--side-bar-bg-color); }
.md-lang { color: rgb(180, 101, 77); }
.html-for-mac .context-menu { --item-hover-bg-color: #E6F0FE; }
#md-notification .btn { border: 0px; }
.dropdown-menu .divider { border-color: rgb(229, 229, 229); }





 .typora-export li, .typora-export p, .typora-export,  .footnote-line {white-space: normal;} 
</style>
</head>
<body class='typora-export os-windows' >
<div  id='write'  class = 'is-node'><p>&nbsp;</p><h1><a name='header-n3' class='md-header-anchor '></a>Why Typora?</h1><p><mark>Readable &amp; Writable</mark></p><p>Typora will give you a seamless experience as both a reader and a writer. It removes the preview window, mode switcher, syntax symbols of markdown source code, and all other unnecessary distractions. Replace them with a real live preview feature to help you concentrate the content itself.</p><h1><a name='header-n6' class='md-header-anchor '></a>Its characteristics</h1><ol start='' ><li>完全免费，目前已支持中文</li><li>跨平台，支持windows,mac,linux</li><li>支持数学公式输入，图片插入</li><li>极其简洁，无多余功能</li><li>界面所见即所得</li></ol><p>&nbsp;</p><h1><a name='header-n19' class='md-header-anchor '></a>区域元素</h1><h2><a name='header-n20' class='md-header-anchor '></a>YAML FONT Matters</h2><p>在文章最上方输入---，按换行键产生，输入内容即可</p><p>&nbsp;</p><h2><a name='header-n23' class='md-header-anchor '></a>菜单</h2><p>输入[toc]+换行键，产生标题，自动更新</p><pre spellcheck="false" class="md-fences md-end-block ty-contain-cm modeLoaded" lang=""><div class="CodeMirror cm-s-inner CodeMirror-wrap" lang=""><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 0px; left: 8px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: 0px; border-right-width: 0px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-code" role="presentation"><div class="CodeMirror-activeline" style="position: relative;"><div class="CodeMirror-activeline-background CodeMirror-linebackground"></div><div class="CodeMirror-gutter-background CodeMirror-activeline-gutter" style="left: 0px; width: 0px;"></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">[toc]</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 0px; width: 1px; border-bottom: 0px solid transparent; top: 22px;"></div><div class="CodeMirror-gutters" style="display: none; height: 22px;"></div></div></div></pre><h3><a name='header-n26' class='md-header-anchor '></a>效果</h3><div class='md-toc' mdtype='toc'><p class="md-toc-content"><span class="md-toc-item md-toc-h1" data-ref="n3"><a class="md-toc-inner" href="#header-n3">Why Typora?</a></span><span class="md-toc-item md-toc-h1" data-ref="n6"><a class="md-toc-inner" href="#header-n6">Its characteristics</a></span><span class="md-toc-item md-toc-h1" data-ref="n19"><a class="md-toc-inner" href="#header-n19">区域元素</a></span><span class="md-toc-item md-toc-h2" data-ref="n20"><a class="md-toc-inner" href="#header-n20">YAML FONT Matters</a></span><span class="md-toc-item md-toc-h2" data-ref="n23"><a class="md-toc-inner" href="#header-n23">菜单</a></span><span class="md-toc-item md-toc-h3" data-ref="n26"><a class="md-toc-inner" href="#header-n26">效果</a></span><span class="md-toc-item md-toc-h2" data-ref="n29"><a class="md-toc-inner" href="#header-n29">段落</a></span><span class="md-toc-item md-toc-h2" data-ref="n33"><a class="md-toc-inner" href="#header-n33">标题</a></span><span class="md-toc-item md-toc-h2" data-ref="n37"><a class="md-toc-inner" href="#header-n37">引注</a></span><span class="md-toc-item md-toc-h3" data-ref="n39"><a class="md-toc-inner" href="#header-n39">效果</a></span><span class="md-toc-item md-toc-h2" data-ref="n47"><a class="md-toc-inner" href="#header-n47">序列</a></span><span class="md-toc-item md-toc-h2" data-ref="n52"><a class="md-toc-inner" href="#header-n52">代码块</a></span><span class="md-toc-item md-toc-h2" data-ref="n56"><a class="md-toc-inner" href="#header-n56">数学块</a></span><span class="md-toc-item md-toc-h2" data-ref="n61"><a class="md-toc-inner" href="#header-n61">表格</a></span><span class="md-toc-item md-toc-h2" data-ref="n73"><a class="md-toc-inner" href="#header-n73">脚注</a></span><span class="md-toc-item md-toc-h2" data-ref="n78"><a class="md-toc-inner" href="#header-n78">水平线</a></span><span class="md-toc-item md-toc-h1" data-ref="n83"><a class="md-toc-inner" href="#header-n83">特征元素</a></span><span class="md-toc-item md-toc-h2" data-ref="n85"><a class="md-toc-inner" href="#header-n85">超链接</a></span><span class="md-toc-item md-toc-h2" data-ref="n91"><a class="md-toc-inner" href="#header-n91">URLs</a></span><span class="md-toc-item md-toc-h2" data-ref="n98"><a class="md-toc-inner" href="#header-n98">图片</a></span><span class="md-toc-item md-toc-h2" data-ref="n109"><a class="md-toc-inner" href="#header-n109">斜体</a></span><span class="md-toc-item md-toc-h2" data-ref="n114"><a class="md-toc-inner" href="#header-n114">加粗</a></span><span class="md-toc-item md-toc-h2" data-ref="n119"><a class="md-toc-inner" href="#header-n119">删除线</a></span><span class="md-toc-item md-toc-h2" data-ref="n124"><a class="md-toc-inner" href="#header-n124">下划线</a></span><span class="md-toc-item md-toc-h2" data-ref="n129"><a class="md-toc-inner" href="#header-n129">代码</a></span><span class="md-toc-item md-toc-h2" data-ref="n134"><a class="md-toc-inner" href="#header-n134"><code>Preference</code> Panel -&gt; <code>Markdown</code> Tab启动</a></span><span class="md-toc-item md-toc-h2" data-ref="n137"><a class="md-toc-inner" href="#header-n137">数学式</a></span><span class="md-toc-item md-toc-h2" data-ref="n143"><a class="md-toc-inner" href="#header-n143">下标</a></span><span class="md-toc-item md-toc-h2" data-ref="n149"><a class="md-toc-inner" href="#header-n149">上标</a></span><span class="md-toc-item md-toc-h2" data-ref="n155"><a class="md-toc-inner" href="#header-n155">高亮</a></span><span class="md-toc-item md-toc-h1" data-ref="n161"><a class="md-toc-inner" href="#header-n161">其他</a></span></p></div><p>&nbsp;</p><h2><a name='header-n29' class='md-header-anchor '></a>段落</h2><p>按换行键建立新的一行
可在行尾插入打断线，禁止向后插入</p><pre spellcheck="false" class="md-fences md-end-block ty-contain-cm modeLoaded" lang=""><div class="CodeMirror cm-s-inner CodeMirror-wrap" lang=""><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 0px; left: 8px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: 0px; border-right-width: 0px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-code" role="presentation"><div class="CodeMirror-activeline" style="position: relative;"><div class="CodeMirror-activeline-background CodeMirror-linebackground"></div><div class="CodeMirror-gutter-background CodeMirror-activeline-gutter" style="left: 0px; width: 0px;"></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">按换行键建立新的一行&lt;br/&gt;</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 0px; width: 1px; border-bottom: 0px solid transparent; top: 22px;"></div><div class="CodeMirror-gutters" style="display: none; height: 22px;"></div></div></div></pre><p>&nbsp;</p><h2><a name='header-n33' class='md-header-anchor '></a>标题</h2><p>开头#的个数表示，空格+文字。标题有1~6个级别，#表示开始，按换行键结束</p><pre spellcheck="false" class="md-fences md-end-block ty-contain-cm modeLoaded" lang=""><div class="CodeMirror cm-s-inner CodeMirror-wrap" lang=""><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 0px; left: 8px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: 0px; border-right-width: 0px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-code" role="presentation"><div class="CodeMirror-activeline" style="position: relative;"><div class="CodeMirror-activeline-background CodeMirror-linebackground"></div><div class="CodeMirror-gutter-background CodeMirror-activeline-gutter" style="left: 0px; width: 0px;"></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"># H1</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">## H2</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">###### H6</span></pre></div></div></div></div></div><div style="position: absolute; height: 0px; width: 1px; border-bottom: 0px solid transparent; top: 67px;"></div><div class="CodeMirror-gutters" style="display: none; height: 67px;"></div></div></div></pre><p>&nbsp;</p><h2><a name='header-n37' class='md-header-anchor '></a>引注</h2><pre spellcheck="false" class="md-fences md-end-block ty-contain-cm modeLoaded" lang=""><div class="CodeMirror cm-s-inner CodeMirror-wrap" lang=""><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 0px; left: 8px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: 0px; border-right-width: 0px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-code" role="presentation"><div class="CodeMirror-activeline" style="position: relative;"><div class="CodeMirror-activeline-background CodeMirror-linebackground"></div><div class="CodeMirror-gutter-background CodeMirror-activeline-gutter" style="left: 0px; width: 0px;"></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">&gt; ni</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">&gt;</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">&gt; ni hao</span></pre></div></div></div></div></div><div style="position: absolute; height: 0px; width: 1px; border-bottom: 0px solid transparent; top: 67px;"></div><div class="CodeMirror-gutters" style="display: none; height: 67px;"></div></div></div></pre><h3><a name='header-n39' class='md-header-anchor '></a>效果</h3><blockquote><p>ni</p><blockquote><p>&nbsp;</p><blockquote><p>nihao</p></blockquote></blockquote></blockquote><p>&nbsp;</p><h2><a name='header-n47' class='md-header-anchor '></a>序列</h2><p>开头*/+/-，空格+文字，可以创建无序序列，换行键换行，删除键+shift+tab跳出</p><p>开头1.，空格+后接文字，可以创建有序序列</p><pre spellcheck="false" class="md-fences md-end-block ty-contain-cm modeLoaded" lang=""><div class="CodeMirror cm-s-inner CodeMirror-wrap" lang=""><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 0px; left: 8px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: 0px; border-right-width: 0px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-code" role="presentation" style=""><div class="CodeMirror-activeline" style="position: relative;"><div class="CodeMirror-activeline-background CodeMirror-linebackground"></div><div class="CodeMirror-gutter-background CodeMirror-activeline-gutter" style="left: 0px; width: 0px;"></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">* &nbsp; Red</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">+ &nbsp; Green</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">- &nbsp; Blue</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"> </span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">1.  Red</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">2.  Green</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">3.  Blue</span></pre></div></div></div></div></div><div style="position: absolute; height: 0px; width: 1px; border-bottom: 0px solid transparent; top: 157px;"></div><div class="CodeMirror-gutters" style="display: none; height: 157px;"></div></div></div></pre><p>&nbsp;</p><h2><a name='header-n52' class='md-header-anchor '></a>代码块</h2><p>开头```+语言名，开启代码块，换行键换行，光标下移键跳出</p><pre spellcheck="false" class="md-fences md-end-block ty-contain-cm modeLoaded" lang=""><div class="CodeMirror cm-s-inner CodeMirror-wrap" lang=""><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 0px; left: 8px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: 0px; border-right-width: 0px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-code" role="presentation"><div class="CodeMirror-activeline" style="position: relative;"><div class="CodeMirror-activeline-background CodeMirror-linebackground"></div><div class="CodeMirror-gutter-background CodeMirror-activeline-gutter" style="left: 0px; width: 0px;"></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">```python</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 0px; width: 1px; border-bottom: 0px solid transparent; top: 22px;"></div><div class="CodeMirror-gutters" style="display: none; height: 22px;"></div></div></div></pre><p>&nbsp;</p><h2><a name='header-n56' class='md-header-anchor '></a>数学块</h2><p>使用MtathJax建立数学公式</p><p>开头$$+换行键，产生输入区域，输入Tex/LaTex格式的数学公式</p><pre spellcheck="false" class="md-fences md-end-block ty-contain-cm modeLoaded" lang=""><div class="CodeMirror cm-s-inner CodeMirror-wrap" lang=""><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 0px; left: 8px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: 0px; border-right-width: 0px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><span><span>​</span>x</span></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-code" role="presentation"><div class="CodeMirror-activeline" style="position: relative;"><div class="CodeMirror-activeline-background CodeMirror-linebackground"></div><div class="CodeMirror-gutter-background CodeMirror-activeline-gutter" style="left: 0px; width: 0px;"></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">$$</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">$$</span></pre></div></div></div></div></div><div style="position: absolute; height: 0px; width: 1px; border-bottom: 0px solid transparent; top: 67px;"></div><div class="CodeMirror-gutters" style="display: none; height: 67px;"></div></div></div></pre><p>&nbsp;</p><h2><a name='header-n61' class='md-header-anchor '></a>表格</h2><p>开头|+列名+|+列名+|+换行键，创建一个2*2表格</p><p>将鼠标放置其上，弹出编辑尺寸，个数，文字等</p><pre spellcheck="false" class="md-fences md-end-block ty-contain-cm modeLoaded" lang=""><div class="CodeMirror cm-s-inner CodeMirror-wrap" lang=""><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 0px; left: 8px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: 0px; border-right-width: 0px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-code" role="presentation"><div class="CodeMirror-activeline" style="position: relative;"><div class="CodeMirror-activeline-background CodeMirror-linebackground"></div><div class="CodeMirror-gutter-background CodeMirror-activeline-gutter" style="left: 0px; width: 0px;"></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">|first|second|</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 0px; width: 1px; border-bottom: 0px solid transparent; top: 22px;"></div><div class="CodeMirror-gutters" style="display: none; height: 22px;"></div></div></div></pre><figure><table><thead><tr><th>first</th><th>second</th></tr></thead><tbody><tr><td>&nbsp;</td><td>&nbsp;</td></tr></tbody></table></figure><p>&nbsp;</p><h2><a name='header-n73' class='md-header-anchor '></a>脚注</h2><p>在需要添加脚注的文字后面+[+^+序列+]，注释的产生可以鼠标放置其上单击自动产生，添加信息</p><p>或人工添加+[+^+序列+]+:</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n76" mdtype="fences">脚注产生的方法[^footnote].
[^footnote]:这个就是*脚注*
</pre><p>&nbsp;</p><h2><a name='header-n78' class='md-header-anchor '></a>水平线</h2><p>输入***/---，换行键换行</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n80" mdtype="fences">***
---
</pre><hr /><hr /><h1><a name='header-n83' class='md-header-anchor '></a>特征元素</h1><p>&nbsp;</p><h2><a name='header-n85' class='md-header-anchor '></a>超链接</h2><p>用[]括住要超链接的内容，紧接着用()括住超链接源+名字，超链接源后面+超链接命名</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n87" mdtype="fences">This is [an example](http://example.com/ "Title") inline link.
 
[This link](http://example.net/) has no title attribute.
</pre><p>This is <a href='http:*//example.com/%20%22Title%22**'>an example</a> inline link.</p><p><a href='http:*//example.net/**'>This link</a> has no title attribute.</p><p>&nbsp;</p><h2><a name='header-n91' class='md-header-anchor '></a>URLs</h2><p>用&lt;&gt;括住url，可手动设置url</p><p>对于标准URLs，可自动识别</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n94" mdtype="fences">&lt;www.Shangzg.top&gt;
www.baidu.com
</pre><p><a href='http://www.Shangzg.top' target='_blank' class='url'>www.Shangzg.top</a></p><p><a href='http://www.baidu.com' target='_blank' class='url'>www.baidu.com</a></p><p>&nbsp;</p><h2><a name='header-n98' class='md-header-anchor '></a>图片</h2><ol start='' ><li>手动添加：类似链接，前面需加！</li><li>用鼠标拖图片进入，然后鼠标放置其上修改</li></ol><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n104" mdtype="fences">![joker](https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-28-How-to-use-Typora/assets/joker.jpg)
</pre><p><img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-28-How-to-use-Typora/assets/joker.jpg" width="70%"></p><p>&nbsp;</p><p>&nbsp;</p><p><img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-28-How-to-use-Typora/assets/illidan.jpg" width="70%"></p><h2><a name='header-n109' class='md-header-anchor '></a>斜体</h2><p>以*或__括住</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n111" mdtype="fences">*Cr7-joker.github.io*
_Cr7-joker.github.io_
</pre><p><em>Cr7-joker.github.io</em>
<em>Cr7-joker.github.io</em></p><p>&nbsp;</p><h2><a name='header-n114' class='md-header-anchor '></a>加粗</h2><p>开头双*或双_，结尾双*或双_，建议双*</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n116" mdtype="fences">**Cr7-joker.github.io**
__Cr7-joker.github.io__
</pre><p><strong>Cr7-joker.github.io</strong>
<strong>Cr7-joker.github.io</strong></p><p>&nbsp;</p><h2><a name='header-n119' class='md-header-anchor '></a>删除线</h2><p>用两个<sub>开头，两个</sub>结尾</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n121" mdtype="fences">~~shangzg.top~~
</pre><p><del>shangzg.top</del></p><p>&nbsp;</p><h2><a name='header-n124' class='md-header-anchor '></a>下划线</h2><p>使用HTML标签</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n126" mdtype="fences">&lt;u&gt;Underline&lt;/u&gt;
</pre><p><u>Underline</u></p><p>&nbsp;</p><h2><a name='header-n129' class='md-header-anchor '></a>代码</h2><p>用两个`在正常段落总表示代码</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n131" mdtype="fences">Use the `printf()` function.
</pre><p>Use the <code>printf()</code> function.</p><p>&nbsp;</p><h2><a name='header-n134' class='md-header-anchor '></a><code>Preference</code> Panel -&gt; <code>Markdown</code> Tab启动</h2><p><img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-28-How-to-use-Typora/assets/markdown.png" width="70%"></p><p>&nbsp;</p><h2><a name='header-n137' class='md-header-anchor '></a>数学式</h2><p>需 <code>Preference</code> Panel -&gt; <code>Markdown</code> Tab启动，</p><p>输入$，然后按ESC键，之后输入Tex命令，可预览</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n140" mdtype="fences">$\lim_{x\to\infty}\exp(-x)=0$
</pre><p><span class="MathJax_SVG" tabindex="-1" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" width="20.819ex" height="2.577ex" viewBox="0 -806.1 8963.9 1109.7" role="img" focusable="false" style="vertical-align: -0.705ex;"><defs><path stroke-width="0" id="E2-MJMAIN-6C" d="M42 46H56Q95 46 103 60V68Q103 77 103 91T103 124T104 167T104 217T104 272T104 329Q104 366 104 407T104 482T104 542T103 586T103 603Q100 622 89 628T44 637H26V660Q26 683 28 683L38 684Q48 685 67 686T104 688Q121 689 141 690T171 693T182 694H185V379Q185 62 186 60Q190 52 198 49Q219 46 247 46H263V0H255L232 1Q209 2 183 2T145 3T107 3T57 1L34 0H26V46H42Z"></path><path stroke-width="0" id="E2-MJMAIN-69" d="M69 609Q69 637 87 653T131 669Q154 667 171 652T188 609Q188 579 171 564T129 549Q104 549 87 564T69 609ZM247 0Q232 3 143 3Q132 3 106 3T56 1L34 0H26V46H42Q70 46 91 49Q100 53 102 60T104 102V205V293Q104 345 102 359T88 378Q74 385 41 385H30V408Q30 431 32 431L42 432Q52 433 70 434T106 436Q123 437 142 438T171 441T182 442H185V62Q190 52 197 50T232 46H255V0H247Z"></path><path stroke-width="0" id="E2-MJMAIN-6D" d="M41 46H55Q94 46 102 60V68Q102 77 102 91T102 122T103 161T103 203Q103 234 103 269T102 328V351Q99 370 88 376T43 385H25V408Q25 431 27 431L37 432Q47 433 65 434T102 436Q119 437 138 438T167 441T178 442H181V402Q181 364 182 364T187 369T199 384T218 402T247 421T285 437Q305 442 336 442Q351 442 364 440T387 434T406 426T421 417T432 406T441 395T448 384T452 374T455 366L457 361L460 365Q463 369 466 373T475 384T488 397T503 410T523 422T546 432T572 439T603 442Q729 442 740 329Q741 322 741 190V104Q741 66 743 59T754 49Q775 46 803 46H819V0H811L788 1Q764 2 737 2T699 3Q596 3 587 0H579V46H595Q656 46 656 62Q657 64 657 200Q656 335 655 343Q649 371 635 385T611 402T585 404Q540 404 506 370Q479 343 472 315T464 232V168V108Q464 78 465 68T468 55T477 49Q498 46 526 46H542V0H534L510 1Q487 2 460 2T422 3Q319 3 310 0H302V46H318Q379 46 379 62Q380 64 380 200Q379 335 378 343Q372 371 358 385T334 402T308 404Q263 404 229 370Q202 343 195 315T187 232V168V108Q187 78 188 68T191 55T200 49Q221 46 249 46H265V0H257L234 1Q210 2 183 2T145 3Q42 3 33 0H25V46H41Z"></path><path stroke-width="0" id="E2-MJMATHI-78" d="M52 289Q59 331 106 386T222 442Q257 442 286 424T329 379Q371 442 430 442Q467 442 494 420T522 361Q522 332 508 314T481 292T458 288Q439 288 427 299T415 328Q415 374 465 391Q454 404 425 404Q412 404 406 402Q368 386 350 336Q290 115 290 78Q290 50 306 38T341 26Q378 26 414 59T463 140Q466 150 469 151T485 153H489Q504 153 504 145Q504 144 502 134Q486 77 440 33T333 -11Q263 -11 227 52Q186 -10 133 -10H127Q78 -10 57 16T35 71Q35 103 54 123T99 143Q142 143 142 101Q142 81 130 66T107 46T94 41L91 40Q91 39 97 36T113 29T132 26Q168 26 194 71Q203 87 217 139T245 247T261 313Q266 340 266 352Q266 380 251 392T217 404Q177 404 142 372T93 290Q91 281 88 280T72 278H58Q52 284 52 289Z"></path><path stroke-width="0" id="E2-MJMAIN-2192" d="M56 237T56 250T70 270H835Q719 357 692 493Q692 494 692 496T691 499Q691 511 708 511H711Q720 511 723 510T729 506T732 497T735 481T743 456Q765 389 816 336T935 261Q944 258 944 250Q944 244 939 241T915 231T877 212Q836 186 806 152T761 85T740 35T732 4Q730 -6 727 -8T711 -11Q691 -11 691 0Q691 7 696 25Q728 151 835 230H70Q56 237 56 250Z"></path><path stroke-width="0" id="E2-MJMAIN-221E" d="M55 217Q55 305 111 373T254 442Q342 442 419 381Q457 350 493 303L507 284L514 294Q618 442 747 442Q833 442 888 374T944 214Q944 128 889 59T743 -11Q657 -11 580 50Q542 81 506 128L492 147L485 137Q381 -11 252 -11Q166 -11 111 57T55 217ZM907 217Q907 285 869 341T761 397Q740 397 720 392T682 378T648 359T619 335T594 310T574 285T559 263T548 246L543 238L574 198Q605 158 622 138T664 94T714 61T765 51Q827 51 867 100T907 217ZM92 214Q92 145 131 89T239 33Q357 33 456 193L425 233Q364 312 334 337Q285 380 233 380Q171 380 132 331T92 214Z"></path><path stroke-width="0" id="E2-MJMAIN-65" d="M28 218Q28 273 48 318T98 391T163 433T229 448Q282 448 320 430T378 380T406 316T415 245Q415 238 408 231H126V216Q126 68 226 36Q246 30 270 30Q312 30 342 62Q359 79 369 104L379 128Q382 131 395 131H398Q415 131 415 121Q415 117 412 108Q393 53 349 21T250 -11Q155 -11 92 58T28 218ZM333 275Q322 403 238 411H236Q228 411 220 410T195 402T166 381T143 340T127 274V267H333V275Z"></path><path stroke-width="0" id="E2-MJMAIN-78" d="M201 0Q189 3 102 3Q26 3 17 0H11V46H25Q48 47 67 52T96 61T121 78T139 96T160 122T180 150L226 210L168 288Q159 301 149 315T133 336T122 351T113 363T107 370T100 376T94 379T88 381T80 383Q74 383 44 385H16V431H23Q59 429 126 429Q219 429 229 431H237V385Q201 381 201 369Q201 367 211 353T239 315T268 274L272 270L297 304Q329 345 329 358Q329 364 327 369T322 376T317 380T310 384L307 385H302V431H309Q324 428 408 428Q487 428 493 431H499V385H492Q443 385 411 368Q394 360 377 341T312 257L296 236L358 151Q424 61 429 57T446 50Q464 46 499 46H516V0H510H502Q494 1 482 1T457 2T432 2T414 3Q403 3 377 3T327 1L304 0H295V46H298Q309 46 320 51T331 63Q331 65 291 120L250 175Q249 174 219 133T185 88Q181 83 181 74Q181 63 188 55T206 46Q208 46 208 23V0H201Z"></path><path stroke-width="0" id="E2-MJMAIN-70" d="M36 -148H50Q89 -148 97 -134V-126Q97 -119 97 -107T97 -77T98 -38T98 6T98 55T98 106Q98 140 98 177T98 243T98 296T97 335T97 351Q94 370 83 376T38 385H20V408Q20 431 22 431L32 432Q42 433 61 434T98 436Q115 437 135 438T165 441T176 442H179V416L180 390L188 397Q247 441 326 441Q407 441 464 377T522 216Q522 115 457 52T310 -11Q242 -11 190 33L182 40V-45V-101Q182 -128 184 -134T195 -145Q216 -148 244 -148H260V-194H252L228 -193Q205 -192 178 -192T140 -191Q37 -191 28 -194H20V-148H36ZM424 218Q424 292 390 347T305 402Q234 402 182 337V98Q222 26 294 26Q345 26 384 80T424 218Z"></path><path stroke-width="0" id="E2-MJMAIN-28" d="M94 250Q94 319 104 381T127 488T164 576T202 643T244 695T277 729T302 750H315H319Q333 750 333 741Q333 738 316 720T275 667T226 581T184 443T167 250T184 58T225 -81T274 -167T316 -220T333 -241Q333 -250 318 -250H315H302L274 -226Q180 -141 137 -14T94 250Z"></path><path stroke-width="0" id="E2-MJMAIN-2212" d="M84 237T84 250T98 270H679Q694 262 694 250T679 230H98Q84 237 84 250Z"></path><path stroke-width="0" id="E2-MJMAIN-29" d="M60 749L64 750Q69 750 74 750H86L114 726Q208 641 251 514T294 250Q294 182 284 119T261 12T224 -76T186 -143T145 -194T113 -227T90 -246Q87 -249 86 -250H74Q66 -250 63 -250T58 -247T55 -238Q56 -237 66 -225Q221 -64 221 250T66 725Q56 737 55 738Q55 746 60 749Z"></path><path stroke-width="0" id="E2-MJMAIN-3D" d="M56 347Q56 360 70 367H707Q722 359 722 347Q722 336 708 328L390 327H72Q56 332 56 347ZM56 153Q56 168 72 173H708Q722 163 722 153Q722 140 707 133H70Q56 140 56 153Z"></path><path stroke-width="0" id="E2-MJMAIN-30" d="M96 585Q152 666 249 666Q297 666 345 640T423 548Q460 465 460 320Q460 165 417 83Q397 41 362 16T301 -15T250 -22Q224 -22 198 -16T137 16T82 83Q39 165 39 320Q39 494 96 585ZM321 597Q291 629 250 629Q208 629 178 597Q153 571 145 525T137 333Q137 175 145 125T181 46Q209 16 250 16Q290 16 318 46Q347 76 354 130T362 333Q362 478 354 524T321 597Z"></path></defs><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xlink:href="#E2-MJMAIN-6C"></use><use xlink:href="#E2-MJMAIN-69" x="278" y="0"></use><use xlink:href="#E2-MJMAIN-6D" x="556" y="0"></use><g transform="translate(1389,-150)"><use transform="scale(0.707)" xlink:href="#E2-MJMATHI-78" x="0" y="0"></use><use transform="scale(0.707)" xlink:href="#E2-MJMAIN-2192" x="572" y="0"></use><use transform="scale(0.707)" xlink:href="#E2-MJMAIN-221E" x="1572" y="0"></use></g><g transform="translate(3474,0)"><use xlink:href="#E2-MJMAIN-65"></use><use xlink:href="#E2-MJMAIN-78" x="444" y="0"></use><use xlink:href="#E2-MJMAIN-70" x="972" y="0"></use></g><use xlink:href="#E2-MJMAIN-28" x="5002" y="0"></use><use xlink:href="#E2-MJMAIN-2212" x="5391" y="0"></use><use xlink:href="#E2-MJMATHI-78" x="6169" y="0"></use><use xlink:href="#E2-MJMAIN-29" x="6741" y="0"></use><use xlink:href="#E2-MJMAIN-3D" x="7408" y="0"></use><use xlink:href="#E2-MJMAIN-30" x="8463" y="0"></use></g></svg></span><script type="math/tex">\lim_{x\to\infty}\exp(-x)=0</script></p><p>&nbsp;</p><h2><a name='header-n143' class='md-header-anchor '></a>下标</h2><p>需 <code>Preference</code> Panel -&gt; <code>Markdown</code> Tab启动，</p><p>使用~括住内容</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n146" mdtype="fences">H~2~O
</pre><p>H<sub>2</sub>O</p><p>&nbsp;</p><h2><a name='header-n149' class='md-header-anchor '></a>上标</h2><p>需 <code>Preference</code> Panel -&gt; <code>Markdown</code> Tab启动，</p><p>使用^括住内容</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n152" mdtype="fences">X^2^
</pre><p>X<sup>2</sup></p><p>&nbsp;</p><h2><a name='header-n155' class='md-header-anchor '></a>高亮</h2><p>需 <code>Preference</code> Panel -&gt; <code>Markdown</code> Tab启动，</p><p>使用==括住内容</p><pre spellcheck="false" class="md-fences mock-cm md-end-block" lang="" contenteditable="false" cid="n158" mdtype="fences">==highlight==
</pre><p><mark>highlight</mark></p><p>&nbsp;</p><h1><a name='header-n161' class='md-header-anchor '></a>其他</h1><p>其实也可以通过鼠标右击完成，选项都有</p><p><img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-28-How-to-use-Typora/assets/other.png" width="70%"></p><p>&nbsp;</p></div>
</body>
</html>
