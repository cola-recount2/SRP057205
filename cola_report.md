cola Report for recount2:SRP057205
==================

**Date**: 2019-12-26 00:56:40 CET, **cola version**: 1.3.2

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary





All available functions which can be applied to this `res_list` object:


```r
res_list
```

```
#> A 'ConsensusPartitionList' object with 24 methods.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows are extracted by 'SD, CV, MAD, ATC' methods.
#>   Subgroups are detected by 'hclust, kmeans, skmeans, pam, mclust, NMF' method.
#>   Number of partitions are tried for k = 2, 3, 4, 5, 6.
#>   Performed in total 30000 partitions by row resampling.
#> 
#> Following methods can be applied to this 'ConsensusPartitionList' object:
#>  [1] "cola_report"           "collect_classes"       "collect_plots"         "collect_stats"        
#>  [5] "colnames"              "functional_enrichment" "get_anno_col"          "get_anno"             
#>  [9] "get_classes"           "get_matrix"            "get_membership"        "get_stats"            
#> [13] "is_best_k"             "is_stable_k"           "ncol"                  "nrow"                 
#> [17] "rownames"              "show"                  "suggest_best_k"        "test_to_known_factors"
#> [21] "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single method by, e.g. object["SD", "hclust"] or object["SD:hclust"]
#> or a subset of methods by object[c("SD", "CV")], c("hclust", "kmeans")]
```

The call of `run_all_consensus_partition_methods()` was:


```
#> run_all_consensus_partition_methods(data = mat, mc.cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_list)
dim(mat)
```

```
#> [1] 13917    56
```

### Density distribution

The density distribution for each sample is visualized as in one column in the
following heatmap. The clustering is based on the distance which is the
Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 4)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)





### Suggest the best k



Folowing table shows the best `k` (number of partitions) for each combination
of top-value methods and partition methods. Clicking on the method name in
the table goes to the section for a single combination of methods.

[The cola vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.


```r
suggest_best_k(res_list)
```


|                            | The best k| 1-PAC| Mean silhouette| Concordance|   |Optional k |
|:---------------------------|----------:|-----:|---------------:|-----------:|:--|:----------|
|[SD:skmeans](#SD-skmeans)   |          4| 1.000|           1.000|       1.000|** |           |
|[SD:NMF](#SD-NMF)           |          2| 1.000|           0.981|       0.991|** |           |
|[CV:hclust](#CV-hclust)     |          2| 1.000|           0.975|       0.986|** |           |
|[MAD:skmeans](#MAD-skmeans) |          4| 1.000|           0.975|       0.978|** |3          |
|[ATC:hclust](#ATC-hclust)   |          2| 1.000|           0.951|       0.979|** |           |
|[ATC:skmeans](#ATC-skmeans) |          2| 1.000|           0.955|       0.983|** |           |
|[ATC:pam](#ATC-pam)         |          3| 1.000|           0.960|       0.982|** |2          |
|[ATC:mclust](#ATC-mclust)   |          2| 1.000|           0.982|       0.988|** |           |
|[MAD:pam](#MAD-pam)         |          5| 0.975|           0.942|       0.972|** |4          |
|[CV:pam](#CV-pam)           |          5| 0.971|           0.937|       0.975|** |2          |
|[ATC:NMF](#ATC-NMF)         |          4| 0.971|           0.937|       0.966|** |           |
|[SD:mclust](#SD-mclust)     |          6| 0.919|           0.883|       0.931|*  |4,5        |
|[CV:NMF](#CV-NMF)           |          4| 0.917|           0.966|       0.951|*  |2,3        |
|[SD:pam](#SD-pam)           |          6| 0.915|           0.893|       0.908|*  |5          |
|[MAD:mclust](#MAD-mclust)   |          6| 0.905|           0.848|       0.880|*  |2,4,5      |
|[MAD:NMF](#MAD-NMF)         |          2| 0.890|           0.913|       0.966|   |           |
|[CV:skmeans](#CV-skmeans)   |          2| 0.805|           0.911|       0.957|   |           |
|[SD:hclust](#SD-hclust)     |          4| 0.665|           0.776|       0.827|   |           |
|[MAD:hclust](#MAD-hclust)   |          3| 0.642|           0.806|       0.864|   |           |
|[ATC:kmeans](#ATC-kmeans)   |          2| 0.539|           0.896|       0.939|   |           |
|[MAD:kmeans](#MAD-kmeans)   |          2| 0.522|           0.794|       0.899|   |           |
|[CV:kmeans](#CV-kmeans)     |          3| 0.433|           0.671|       0.783|   |           |
|[SD:kmeans](#SD-kmeans)     |          2| 0.399|           0.747|       0.873|   |           |
|[CV:mclust](#CV-mclust)     |          2| 0.384|           0.811|       0.859|   |           |

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9




### CDF of consensus matrices

Cumulative distribution function curves of consensus matrix for all methods.




```r
collect_plots(res_list, fun = plot_ecdf)
```

![plot of chunk collect-plots](figure_cola/collect-plots-1.png)



### Consensus heatmap

Consensus heatmaps for all methods. ([What is a consensus heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_9))


<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-consensus-heatmap'>
<ul>
<li><a href='#tab-collect-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-consensus-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-1-1.png" alt="plot of chunk tab-collect-consensus-heatmap-1"/></p>

</div>
<div id='tab-collect-consensus-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-2-1.png" alt="plot of chunk tab-collect-consensus-heatmap-2"/></p>

</div>
<div id='tab-collect-consensus-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-3-1.png" alt="plot of chunk tab-collect-consensus-heatmap-3"/></p>

</div>
<div id='tab-collect-consensus-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-4-1.png" alt="plot of chunk tab-collect-consensus-heatmap-4"/></p>

</div>
<div id='tab-collect-consensus-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-5-1.png" alt="plot of chunk tab-collect-consensus-heatmap-5"/></p>

</div>
</div>



### Membership heatmap

Membership heatmaps for all methods. ([What is a membership heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_12))


<script>
$( function() {
	$( '#tabs-collect-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-membership-heatmap'>
<ul>
<li><a href='#tab-collect-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-membership-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-1-1.png" alt="plot of chunk tab-collect-membership-heatmap-1"/></p>

</div>
<div id='tab-collect-membership-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-2-1.png" alt="plot of chunk tab-collect-membership-heatmap-2"/></p>

</div>
<div id='tab-collect-membership-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-3-1.png" alt="plot of chunk tab-collect-membership-heatmap-3"/></p>

</div>
<div id='tab-collect-membership-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-4-1.png" alt="plot of chunk tab-collect-membership-heatmap-4"/></p>

</div>
<div id='tab-collect-membership-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-5-1.png" alt="plot of chunk tab-collect-membership-heatmap-5"/></p>

</div>
</div>



### Signature heatmap

Signature heatmaps for all methods. ([What is a signature heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_22))


Note in following heatmaps, rows are scaled.



<script>
$( function() {
	$( '#tabs-collect-get-signatures' ).tabs();
} );
</script>
<div id='tabs-collect-get-signatures'>
<ul>
<li><a href='#tab-collect-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-collect-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-collect-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-collect-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-collect-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-collect-get-signatures-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-1-1.png" alt="plot of chunk tab-collect-get-signatures-1"/></p>

</div>
<div id='tab-collect-get-signatures-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-2-1.png" alt="plot of chunk tab-collect-get-signatures-2"/></p>

</div>
<div id='tab-collect-get-signatures-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-3-1.png" alt="plot of chunk tab-collect-get-signatures-3"/></p>

</div>
<div id='tab-collect-get-signatures-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-4-1.png" alt="plot of chunk tab-collect-get-signatures-4"/></p>

</div>
<div id='tab-collect-get-signatures-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-5-1.png" alt="plot of chunk tab-collect-get-signatures-5"/></p>

</div>
</div>



### Statistics table

The statistics used for measuring the stability of consensus partitioning.
([How are they
defined?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13))


<script>
$( function() {
	$( '#tabs-get-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-get-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-get-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-get-stats-from-consensus-partition-list-1'>
<pre><code class="r">get_stats(res_list, k = 2)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      2 1.000           0.981       0.991          0.509 0.491   0.491
#&gt; CV:NMF      2 1.000           0.998       0.999          0.469 0.532   0.532
#&gt; MAD:NMF     2 0.890           0.913       0.966          0.507 0.492   0.492
#&gt; ATC:NMF     2 0.285           0.629       0.736          0.446 0.532   0.532
#&gt; SD:skmeans  2 0.545           0.576       0.844          0.508 0.491   0.491
#&gt; CV:skmeans  2 0.805           0.911       0.957          0.465 0.556   0.556
#&gt; MAD:skmeans 2 0.860           0.861       0.943          0.508 0.491   0.491
#&gt; ATC:skmeans 2 1.000           0.955       0.983          0.503 0.501   0.501
#&gt; SD:mclust   2 0.532           0.944       0.955          0.363 0.657   0.657
#&gt; CV:mclust   2 0.384           0.811       0.859          0.466 0.532   0.532
#&gt; MAD:mclust  2 1.000           1.000       1.000          0.344 0.657   0.657
#&gt; ATC:mclust  2 1.000           0.982       0.988          0.421 0.584   0.584
#&gt; SD:kmeans   2 0.399           0.747       0.873          0.468 0.556   0.556
#&gt; CV:kmeans   2 0.419           0.860       0.879          0.345 0.618   0.618
#&gt; MAD:kmeans  2 0.522           0.794       0.899          0.481 0.514   0.514
#&gt; ATC:kmeans  2 0.539           0.896       0.939          0.435 0.532   0.532
#&gt; SD:pam      2 0.353           0.755       0.854          0.461 0.494   0.494
#&gt; CV:pam      2 0.992           0.981       0.990          0.208 0.805   0.805
#&gt; MAD:pam     2 0.675           0.916       0.951          0.457 0.514   0.514
#&gt; ATC:pam     2 1.000           0.981       0.969          0.482 0.494   0.494
#&gt; SD:hclust   2 0.790           0.893       0.952          0.355 0.618   0.618
#&gt; CV:hclust   2 1.000           0.975       0.986          0.156 0.865   0.865
#&gt; MAD:hclust  2 0.852           0.957       0.972          0.421 0.584   0.584
#&gt; ATC:hclust  2 1.000           0.951       0.979          0.169 0.805   0.805
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-2'>
<pre><code class="r">get_stats(res_list, k = 3)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      3 0.739           0.685       0.876          0.310 0.718   0.485
#&gt; CV:NMF      3 1.000           0.982       0.985          0.400 0.813   0.649
#&gt; MAD:NMF     3 0.648           0.658       0.838          0.301 0.751   0.543
#&gt; ATC:NMF     3 0.871           0.886       0.957          0.423 0.792   0.624
#&gt; SD:skmeans  3 0.670           0.887       0.911          0.315 0.758   0.544
#&gt; CV:skmeans  3 0.678           0.879       0.937          0.411 0.771   0.589
#&gt; MAD:skmeans 3 1.000           0.981       0.991          0.325 0.758   0.544
#&gt; ATC:skmeans 3 0.762           0.884       0.911          0.208 0.883   0.770
#&gt; SD:mclust   3 0.572           0.633       0.825          0.675 0.727   0.585
#&gt; CV:mclust   3 0.562           0.715       0.840          0.372 0.743   0.540
#&gt; MAD:mclust  3 0.597           0.870       0.873          0.791 0.709   0.557
#&gt; ATC:mclust  3 0.441           0.852       0.866          0.224 0.530   0.403
#&gt; SD:kmeans   3 0.505           0.642       0.784          0.396 0.730   0.532
#&gt; CV:kmeans   3 0.433           0.671       0.783          0.589 0.735   0.598
#&gt; MAD:kmeans  3 0.553           0.783       0.841          0.371 0.751   0.543
#&gt; ATC:kmeans  3 0.670           0.767       0.840          0.411 0.774   0.615
#&gt; SD:pam      3 0.467           0.638       0.829          0.394 0.751   0.538
#&gt; CV:pam      3 0.590           0.910       0.935          1.008 0.782   0.729
#&gt; MAD:pam     3 0.797           0.715       0.888          0.451 0.579   0.339
#&gt; ATC:pam     3 1.000           0.960       0.982          0.196 0.922   0.842
#&gt; SD:hclust   3 0.419           0.620       0.779          0.771 0.730   0.563
#&gt; CV:hclust   3 0.433           0.530       0.785          1.839 0.727   0.685
#&gt; MAD:hclust  3 0.642           0.806       0.864          0.533 0.764   0.596
#&gt; ATC:hclust  3 0.869           0.894       0.961          2.382 0.579   0.494
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-3'>
<pre><code class="r">get_stats(res_list, k = 4)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      4 0.824           0.926       0.930         0.1281 0.853   0.587
#&gt; CV:NMF      4 0.917           0.966       0.951         0.1371 0.906   0.729
#&gt; MAD:NMF     4 0.679           0.760       0.847         0.1178 0.756   0.416
#&gt; ATC:NMF     4 0.971           0.937       0.966         0.1543 0.821   0.558
#&gt; SD:skmeans  4 1.000           1.000       1.000         0.1387 0.870   0.627
#&gt; CV:skmeans  4 0.704           0.634       0.848         0.1393 0.836   0.566
#&gt; MAD:skmeans 4 1.000           0.975       0.978         0.1274 0.870   0.627
#&gt; ATC:skmeans 4 0.821           0.880       0.905         0.1320 0.878   0.701
#&gt; SD:mclust   4 0.997           0.975       0.985         0.2499 0.855   0.622
#&gt; CV:mclust   4 0.565           0.722       0.788         0.1251 0.927   0.783
#&gt; MAD:mclust  4 0.932           0.975       0.986         0.2329 0.873   0.652
#&gt; ATC:mclust  4 0.631           0.773       0.887         0.3562 0.725   0.488
#&gt; SD:kmeans   4 0.584           0.823       0.814         0.1251 0.865   0.615
#&gt; CV:kmeans   4 0.433           0.629       0.692         0.2055 0.883   0.741
#&gt; MAD:kmeans  4 0.590           0.682       0.776         0.1118 0.932   0.797
#&gt; ATC:kmeans  4 0.620           0.653       0.784         0.1311 0.852   0.652
#&gt; SD:pam      4 0.845           0.869       0.942         0.1804 0.860   0.609
#&gt; CV:pam      4 0.865           0.925       0.971         0.4110 0.808   0.678
#&gt; MAD:pam     4 0.983           0.945       0.977         0.1469 0.823   0.531
#&gt; ATC:pam     4 0.678           0.672       0.856         0.2110 0.808   0.577
#&gt; SD:hclust   4 0.665           0.776       0.827         0.1826 0.891   0.687
#&gt; CV:hclust   4 0.636           0.731       0.862         0.3908 0.675   0.486
#&gt; MAD:hclust  4 0.748           0.589       0.788         0.1543 0.969   0.910
#&gt; ATC:hclust  4 0.874           0.886       0.960         0.0488 0.953   0.893
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-4'>
<pre><code class="r">get_stats(res_list, k = 5)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      5 0.846           0.792       0.877         0.0555 0.964   0.851
#&gt; CV:NMF      5 0.807           0.682       0.824         0.0639 0.977   0.907
#&gt; MAD:NMF     5 0.645           0.659       0.801         0.0579 0.868   0.549
#&gt; ATC:NMF     5 0.794           0.755       0.854         0.0682 0.958   0.845
#&gt; SD:skmeans  5 0.857           0.717       0.836         0.0537 0.943   0.773
#&gt; CV:skmeans  5 0.720           0.762       0.838         0.0657 0.852   0.517
#&gt; MAD:skmeans 5 0.849           0.771       0.872         0.0577 0.909   0.650
#&gt; ATC:skmeans 5 0.765           0.716       0.851         0.0705 0.982   0.938
#&gt; SD:mclust   5 0.961           0.895       0.956         0.0447 0.945   0.779
#&gt; CV:mclust   5 0.639           0.712       0.725         0.0430 0.948   0.808
#&gt; MAD:mclust  5 0.961           0.927       0.966         0.0491 0.945   0.779
#&gt; ATC:mclust  5 0.796           0.773       0.862         0.0851 0.964   0.870
#&gt; SD:kmeans   5 0.665           0.745       0.779         0.0608 1.000   1.000
#&gt; CV:kmeans   5 0.500           0.529       0.695         0.0960 0.974   0.928
#&gt; MAD:kmeans  5 0.665           0.724       0.776         0.0620 0.922   0.735
#&gt; ATC:kmeans  5 0.606           0.660       0.777         0.0885 0.927   0.769
#&gt; SD:pam      5 1.000           0.980       0.991         0.0585 0.917   0.680
#&gt; CV:pam      5 0.971           0.937       0.975         0.1208 0.906   0.778
#&gt; MAD:pam     5 0.975           0.942       0.972         0.0445 0.927   0.717
#&gt; ATC:pam     5 0.755           0.673       0.831         0.0664 0.844   0.549
#&gt; SD:hclust   5 0.799           0.629       0.800         0.0755 0.906   0.657
#&gt; CV:hclust   5 0.776           0.814       0.898         0.1231 0.917   0.766
#&gt; MAD:hclust  5 0.730           0.659       0.778         0.0602 0.940   0.813
#&gt; ATC:hclust  5 0.816           0.773       0.869         0.1266 0.899   0.748
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-5'>
<pre><code class="r">get_stats(res_list, k = 6)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      6 0.813           0.760       0.847         0.0382 0.958   0.805
#&gt; CV:NMF      6 0.782           0.661       0.781         0.0441 0.906   0.617
#&gt; MAD:NMF     6 0.655           0.623       0.760         0.0364 0.940   0.739
#&gt; ATC:NMF     6 0.757           0.655       0.783         0.0516 0.956   0.813
#&gt; SD:skmeans  6 0.829           0.751       0.835         0.0331 0.938   0.718
#&gt; CV:skmeans  6 0.751           0.660       0.775         0.0438 0.935   0.699
#&gt; MAD:skmeans 6 0.849           0.697       0.834         0.0323 0.953   0.778
#&gt; ATC:skmeans 6 0.723           0.646       0.785         0.0420 0.974   0.907
#&gt; SD:mclust   6 0.919           0.883       0.931         0.0463 0.961   0.805
#&gt; CV:mclust   6 0.744           0.691       0.835         0.0623 0.852   0.482
#&gt; MAD:mclust  6 0.905           0.848       0.880         0.0396 0.922   0.655
#&gt; ATC:mclust  6 0.841           0.821       0.922         0.0646 0.948   0.787
#&gt; SD:kmeans   6 0.712           0.658       0.730         0.0440 0.974   0.891
#&gt; CV:kmeans   6 0.553           0.560       0.668         0.0629 0.925   0.793
#&gt; MAD:kmeans  6 0.670           0.631       0.717         0.0401 0.984   0.935
#&gt; ATC:kmeans  6 0.645           0.543       0.702         0.0512 0.953   0.825
#&gt; SD:pam      6 0.915           0.893       0.908         0.0242 0.969   0.848
#&gt; CV:pam      6 0.950           0.932       0.947         0.0336 0.984   0.953
#&gt; MAD:pam     6 0.897           0.852       0.910         0.0362 0.990   0.949
#&gt; ATC:pam     6 0.884           0.823       0.928         0.0537 0.953   0.811
#&gt; SD:hclust   6 0.844           0.799       0.891         0.0333 0.927   0.678
#&gt; CV:hclust   6 0.726           0.774       0.835         0.1012 0.961   0.862
#&gt; MAD:hclust  6 0.807           0.792       0.851         0.0339 0.917   0.683
#&gt; ATC:hclust  6 0.869           0.861       0.936         0.0412 0.979   0.934
</code></pre>

</div>
</div>

Following heatmap plots the partition for each combination of methods and the
lightness correspond to the silhouette scores for samples in each method. On
top the consensus subgroup is inferred from all methods by taking the mean
silhouette scores as weight.


<script>
$( function() {
	$( '#tabs-collect-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-stats-from-consensus-partition-list-1'>
<pre><code class="r">collect_stats(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-2'>
<pre><code class="r">collect_stats(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-3'>
<pre><code class="r">collect_stats(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-4'>
<pre><code class="r">collect_stats(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-5'>
<pre><code class="r">collect_stats(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-5"/></p>

</div>
</div>

### Partition from all methods



Collect partitions from all methods:


<script>
$( function() {
	$( '#tabs-collect-classes-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-classes-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-classes-from-consensus-partition-list-1'>
<pre><code class="r">collect_classes(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-2'>
<pre><code class="r">collect_classes(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-3'>
<pre><code class="r">collect_classes(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-4'>
<pre><code class="r">collect_classes(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-5'>
<pre><code class="r">collect_classes(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-5"/></p>

</div>
</div>



### Top rows overlap


Overlap of top rows from different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-euler' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-euler'>
<ul>
<li><a href='#tab-top-rows-overlap-by-euler-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-euler-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-5"/></p>

</div>
</div>

Also visualize the correspondance of rankings between different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-correspondance' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-correspondance'>
<ul>
<li><a href='#tab-top-rows-overlap-by-correspondance-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-correspondance-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-5"/></p>

</div>
</div>


Heatmaps of the top rows:



<script>
$( function() {
	$( '#tabs-top-rows-heatmap' ).tabs();
} );
</script>
<div id='tabs-top-rows-heatmap'>
<ul>
<li><a href='#tab-top-rows-heatmap-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-heatmap-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-heatmap-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-heatmap-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-heatmap-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-heatmap-1'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 1000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-1-1.png" alt="plot of chunk tab-top-rows-heatmap-1"/></p>

</div>
<div id='tab-top-rows-heatmap-2'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 2000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-2-1.png" alt="plot of chunk tab-top-rows-heatmap-2"/></p>

</div>
<div id='tab-top-rows-heatmap-3'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 3000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-3-1.png" alt="plot of chunk tab-top-rows-heatmap-3"/></p>

</div>
<div id='tab-top-rows-heatmap-4'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 4000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-4-1.png" alt="plot of chunk tab-top-rows-heatmap-4"/></p>

</div>
<div id='tab-top-rows-heatmap-5'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 5000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-5-1.png" alt="plot of chunk tab-top-rows-heatmap-5"/></p>

</div>
</div>



 
## Results for each method


---------------------------------------------------




### SD:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "hclust"]
# you can also extract it by
# res = res_list["SD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-hclust-collect-plots](figure_cola/SD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-hclust-select-partition-number](figure_cola/SD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.790           0.893       0.952         0.3548 0.618   0.618
#> 3 3 0.419           0.620       0.779         0.7711 0.730   0.563
#> 4 4 0.665           0.776       0.827         0.1826 0.891   0.687
#> 5 5 0.799           0.629       0.800         0.0755 0.906   0.657
#> 6 6 0.844           0.799       0.891         0.0333 0.927   0.678
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-classes'>
<ul>
<li><a href='#tab-SD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-hclust-get-classes-1'>
<p><a id='tab-SD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975507     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975506     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975505     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975503     1  0.5408      0.782 0.876 0.124
#&gt; SRR1975504     1  0.5408      0.782 0.876 0.124
#&gt; SRR1975501     2  0.0376      0.975 0.004 0.996
#&gt; SRR1975502     2  0.0376      0.975 0.004 0.996
#&gt; SRR1975499     1  0.0000      0.841 1.000 0.000
#&gt; SRR1975500     1  0.0000      0.841 1.000 0.000
#&gt; SRR1975497     2  0.0672      0.972 0.008 0.992
#&gt; SRR1975498     2  0.0672      0.972 0.008 0.992
#&gt; SRR1975493     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975494     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975495     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975496     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975491     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975492     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975489     1  0.0000      0.841 1.000 0.000
#&gt; SRR1975490     1  0.0000      0.841 1.000 0.000
#&gt; SRR1975487     1  0.0000      0.841 1.000 0.000
#&gt; SRR1975488     1  0.0000      0.841 1.000 0.000
#&gt; SRR1975485     1  0.0000      0.841 1.000 0.000
#&gt; SRR1975486     1  0.0000      0.841 1.000 0.000
#&gt; SRR1975483     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975484     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975481     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975482     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975477     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975478     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975479     1  0.9710      0.463 0.600 0.400
#&gt; SRR1975480     1  0.9710      0.463 0.600 0.400
#&gt; SRR1975475     1  0.9850      0.400 0.572 0.428
#&gt; SRR1975476     1  0.9850      0.400 0.572 0.428
#&gt; SRR1975473     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975474     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975471     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975472     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975469     2  0.0376      0.975 0.004 0.996
#&gt; SRR1975470     2  0.0376      0.975 0.004 0.996
#&gt; SRR1975467     2  0.8661      0.509 0.288 0.712
#&gt; SRR1975468     2  0.8661      0.509 0.288 0.712
#&gt; SRR1975465     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975466     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975463     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975464     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975461     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975462     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975459     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975460     2  0.1184      0.970 0.016 0.984
#&gt; SRR1975457     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975458     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975455     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975456     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975453     2  0.0000      0.976 0.000 1.000
#&gt; SRR1975454     2  0.0000      0.976 0.000 1.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-1-a').click(function(){
  $('#tab-SD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-2'>
<p><a id='tab-SD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     2  0.6095      0.435 0.000 0.608 0.392
#&gt; SRR1975507     2  0.6095      0.435 0.000 0.608 0.392
#&gt; SRR1975506     2  0.6095      0.435 0.000 0.608 0.392
#&gt; SRR1975505     2  0.6095      0.435 0.000 0.608 0.392
#&gt; SRR1975503     1  0.3826      0.750 0.868 0.008 0.124
#&gt; SRR1975504     1  0.3826      0.750 0.868 0.008 0.124
#&gt; SRR1975501     3  0.5285      0.591 0.004 0.244 0.752
#&gt; SRR1975502     3  0.5285      0.591 0.004 0.244 0.752
#&gt; SRR1975499     1  0.0000      0.836 1.000 0.000 0.000
#&gt; SRR1975500     1  0.0000      0.836 1.000 0.000 0.000
#&gt; SRR1975497     3  0.0424      0.870 0.008 0.000 0.992
#&gt; SRR1975498     3  0.0424      0.870 0.008 0.000 0.992
#&gt; SRR1975493     2  0.5016      0.522 0.000 0.760 0.240
#&gt; SRR1975494     2  0.5016      0.522 0.000 0.760 0.240
#&gt; SRR1975495     3  0.0000      0.875 0.000 0.000 1.000
#&gt; SRR1975496     3  0.0000      0.875 0.000 0.000 1.000
#&gt; SRR1975491     3  0.5465      0.545 0.000 0.288 0.712
#&gt; SRR1975492     3  0.5465      0.545 0.000 0.288 0.712
#&gt; SRR1975489     1  0.0000      0.836 1.000 0.000 0.000
#&gt; SRR1975490     1  0.0000      0.836 1.000 0.000 0.000
#&gt; SRR1975487     1  0.0000      0.836 1.000 0.000 0.000
#&gt; SRR1975488     1  0.0000      0.836 1.000 0.000 0.000
#&gt; SRR1975485     1  0.0000      0.836 1.000 0.000 0.000
#&gt; SRR1975486     1  0.0000      0.836 1.000 0.000 0.000
#&gt; SRR1975483     3  0.0000      0.875 0.000 0.000 1.000
#&gt; SRR1975484     3  0.0000      0.875 0.000 0.000 1.000
#&gt; SRR1975481     3  0.0000      0.875 0.000 0.000 1.000
#&gt; SRR1975482     3  0.0000      0.875 0.000 0.000 1.000
#&gt; SRR1975477     2  0.5465      0.501 0.000 0.712 0.288
#&gt; SRR1975478     2  0.5465      0.501 0.000 0.712 0.288
#&gt; SRR1975479     1  0.8198      0.572 0.596 0.304 0.100
#&gt; SRR1975480     1  0.8198      0.572 0.596 0.304 0.100
#&gt; SRR1975475     1  0.8535      0.523 0.556 0.332 0.112
#&gt; SRR1975476     1  0.8535      0.523 0.556 0.332 0.112
#&gt; SRR1975473     2  0.5465      0.501 0.000 0.712 0.288
#&gt; SRR1975474     2  0.5465      0.501 0.000 0.712 0.288
#&gt; SRR1975471     3  0.0000      0.875 0.000 0.000 1.000
#&gt; SRR1975472     3  0.0000      0.875 0.000 0.000 1.000
#&gt; SRR1975469     3  0.0237      0.873 0.004 0.000 0.996
#&gt; SRR1975470     3  0.0237      0.873 0.004 0.000 0.996
#&gt; SRR1975467     2  0.9528      0.155 0.272 0.488 0.240
#&gt; SRR1975468     2  0.9528      0.155 0.272 0.488 0.240
#&gt; SRR1975465     2  0.5016      0.522 0.000 0.760 0.240
#&gt; SRR1975466     2  0.5016      0.522 0.000 0.760 0.240
#&gt; SRR1975463     2  0.5016      0.522 0.000 0.760 0.240
#&gt; SRR1975464     2  0.5016      0.522 0.000 0.760 0.240
#&gt; SRR1975461     2  0.6095      0.435 0.000 0.608 0.392
#&gt; SRR1975462     2  0.6095      0.435 0.000 0.608 0.392
#&gt; SRR1975459     2  0.5016      0.522 0.000 0.760 0.240
#&gt; SRR1975460     2  0.5016      0.522 0.000 0.760 0.240
#&gt; SRR1975457     2  0.6274      0.408 0.000 0.544 0.456
#&gt; SRR1975458     2  0.6274      0.408 0.000 0.544 0.456
#&gt; SRR1975455     2  0.6274      0.408 0.000 0.544 0.456
#&gt; SRR1975456     2  0.6274      0.408 0.000 0.544 0.456
#&gt; SRR1975453     2  0.6095      0.435 0.000 0.608 0.392
#&gt; SRR1975454     2  0.6095      0.435 0.000 0.608 0.392
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-2-a').click(function(){
  $('#tab-SD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-3'>
<p><a id='tab-SD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3   0.000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR1975507     3   0.000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR1975506     3   0.000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR1975505     3   0.000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR1975503     4   0.281      0.740 0.000 0.132 0.000 0.868
#&gt; SRR1975504     4   0.281      0.740 0.000 0.132 0.000 0.868
#&gt; SRR1975501     1   0.187      0.582 0.928 0.072 0.000 0.000
#&gt; SRR1975502     1   0.187      0.582 0.928 0.072 0.000 0.000
#&gt; SRR1975499     4   0.000      0.841 0.000 0.000 0.000 1.000
#&gt; SRR1975500     4   0.000      0.841 0.000 0.000 0.000 1.000
#&gt; SRR1975497     1   0.384      0.840 0.776 0.000 0.224 0.000
#&gt; SRR1975498     1   0.384      0.840 0.776 0.000 0.224 0.000
#&gt; SRR1975493     2   0.384      0.838 0.224 0.776 0.000 0.000
#&gt; SRR1975494     2   0.384      0.838 0.224 0.776 0.000 0.000
#&gt; SRR1975495     1   0.398      0.847 0.760 0.000 0.240 0.000
#&gt; SRR1975496     1   0.398      0.847 0.760 0.000 0.240 0.000
#&gt; SRR1975491     1   0.413      0.242 0.740 0.260 0.000 0.000
#&gt; SRR1975492     1   0.413      0.242 0.740 0.260 0.000 0.000
#&gt; SRR1975489     4   0.000      0.841 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4   0.000      0.841 0.000 0.000 0.000 1.000
#&gt; SRR1975487     4   0.000      0.841 0.000 0.000 0.000 1.000
#&gt; SRR1975488     4   0.000      0.841 0.000 0.000 0.000 1.000
#&gt; SRR1975485     4   0.000      0.841 0.000 0.000 0.000 1.000
#&gt; SRR1975486     4   0.000      0.841 0.000 0.000 0.000 1.000
#&gt; SRR1975483     1   0.398      0.847 0.760 0.000 0.240 0.000
#&gt; SRR1975484     1   0.398      0.847 0.760 0.000 0.240 0.000
#&gt; SRR1975481     1   0.398      0.847 0.760 0.000 0.240 0.000
#&gt; SRR1975482     1   0.398      0.847 0.760 0.000 0.240 0.000
#&gt; SRR1975477     2   0.284      0.677 0.052 0.900 0.048 0.000
#&gt; SRR1975478     2   0.284      0.677 0.052 0.900 0.048 0.000
#&gt; SRR1975479     4   0.599      0.579 0.052 0.352 0.000 0.596
#&gt; SRR1975480     4   0.599      0.579 0.052 0.352 0.000 0.596
#&gt; SRR1975475     4   0.611      0.522 0.052 0.392 0.000 0.556
#&gt; SRR1975476     4   0.611      0.522 0.052 0.392 0.000 0.556
#&gt; SRR1975473     2   0.284      0.677 0.052 0.900 0.048 0.000
#&gt; SRR1975474     2   0.284      0.677 0.052 0.900 0.048 0.000
#&gt; SRR1975471     1   0.398      0.847 0.760 0.000 0.240 0.000
#&gt; SRR1975472     1   0.398      0.847 0.760 0.000 0.240 0.000
#&gt; SRR1975469     1   0.394      0.846 0.764 0.000 0.236 0.000
#&gt; SRR1975470     1   0.394      0.846 0.764 0.000 0.236 0.000
#&gt; SRR1975467     2   0.746      0.521 0.224 0.504 0.000 0.272
#&gt; SRR1975468     2   0.746      0.521 0.224 0.504 0.000 0.272
#&gt; SRR1975465     2   0.384      0.838 0.224 0.776 0.000 0.000
#&gt; SRR1975466     2   0.384      0.838 0.224 0.776 0.000 0.000
#&gt; SRR1975463     2   0.384      0.838 0.224 0.776 0.000 0.000
#&gt; SRR1975464     2   0.384      0.838 0.224 0.776 0.000 0.000
#&gt; SRR1975461     3   0.000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR1975462     3   0.000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR1975459     2   0.384      0.838 0.224 0.776 0.000 0.000
#&gt; SRR1975460     2   0.384      0.838 0.224 0.776 0.000 0.000
#&gt; SRR1975457     3   0.312      0.848 0.000 0.156 0.844 0.000
#&gt; SRR1975458     3   0.312      0.848 0.000 0.156 0.844 0.000
#&gt; SRR1975455     3   0.312      0.848 0.000 0.156 0.844 0.000
#&gt; SRR1975456     3   0.312      0.848 0.000 0.156 0.844 0.000
#&gt; SRR1975453     3   0.000      0.927 0.000 0.000 1.000 0.000
#&gt; SRR1975454     3   0.000      0.927 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-3-a').click(function(){
  $('#tab-SD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-4'>
<p><a id='tab-SD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.0000     0.9254 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975507     3  0.0000     0.9254 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975506     3  0.0000     0.9254 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975505     3  0.0000     0.9254 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975503     4  0.4341     0.6157 0.000 0.004 0.000 0.592 0.404
#&gt; SRR1975504     4  0.4341     0.6157 0.000 0.004 0.000 0.592 0.404
#&gt; SRR1975501     1  0.4582     0.0171 0.572 0.012 0.000 0.000 0.416
#&gt; SRR1975502     1  0.4582     0.0171 0.572 0.012 0.000 0.000 0.416
#&gt; SRR1975499     4  0.1831     0.8763 0.000 0.004 0.000 0.920 0.076
#&gt; SRR1975500     4  0.1831     0.8763 0.000 0.004 0.000 0.920 0.076
#&gt; SRR1975497     1  0.0566     0.9000 0.984 0.012 0.000 0.000 0.004
#&gt; SRR1975498     1  0.0566     0.9000 0.984 0.012 0.000 0.000 0.004
#&gt; SRR1975493     2  0.4256     0.3289 0.000 0.564 0.000 0.000 0.436
#&gt; SRR1975494     2  0.4256     0.3289 0.000 0.564 0.000 0.000 0.436
#&gt; SRR1975495     1  0.0000     0.9094 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975496     1  0.0000     0.9094 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975491     5  0.4856     0.3897 0.388 0.028 0.000 0.000 0.584
#&gt; SRR1975492     5  0.4856     0.3897 0.388 0.028 0.000 0.000 0.584
#&gt; SRR1975489     4  0.0794     0.8892 0.000 0.000 0.000 0.972 0.028
#&gt; SRR1975490     4  0.0794     0.8892 0.000 0.000 0.000 0.972 0.028
#&gt; SRR1975487     4  0.0000     0.8974 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975488     4  0.0000     0.8974 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975485     4  0.0000     0.8974 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975486     4  0.0000     0.8974 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975483     1  0.0000     0.9094 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000     0.9094 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0000     0.9094 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975482     1  0.0000     0.9094 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975477     2  0.1197     0.3794 0.000 0.952 0.048 0.000 0.000
#&gt; SRR1975478     2  0.1197     0.3794 0.000 0.952 0.048 0.000 0.000
#&gt; SRR1975479     2  0.6706    -0.1397 0.000 0.416 0.000 0.328 0.256
#&gt; SRR1975480     2  0.6706    -0.1397 0.000 0.416 0.000 0.328 0.256
#&gt; SRR1975475     2  0.6598    -0.0871 0.000 0.452 0.000 0.316 0.232
#&gt; SRR1975476     2  0.6598    -0.0871 0.000 0.452 0.000 0.316 0.232
#&gt; SRR1975473     2  0.1197     0.3794 0.000 0.952 0.048 0.000 0.000
#&gt; SRR1975474     2  0.1197     0.3794 0.000 0.952 0.048 0.000 0.000
#&gt; SRR1975471     1  0.0000     0.9094 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975472     1  0.0000     0.9094 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975469     1  0.0162     0.9078 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1975470     1  0.0162     0.9078 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1975467     5  0.2773     0.3290 0.000 0.164 0.000 0.000 0.836
#&gt; SRR1975468     5  0.2773     0.3290 0.000 0.164 0.000 0.000 0.836
#&gt; SRR1975465     2  0.4256     0.3289 0.000 0.564 0.000 0.000 0.436
#&gt; SRR1975466     2  0.4256     0.3289 0.000 0.564 0.000 0.000 0.436
#&gt; SRR1975463     2  0.4256     0.3289 0.000 0.564 0.000 0.000 0.436
#&gt; SRR1975464     2  0.4256     0.3289 0.000 0.564 0.000 0.000 0.436
#&gt; SRR1975461     3  0.0510     0.9225 0.016 0.000 0.984 0.000 0.000
#&gt; SRR1975462     3  0.0510     0.9225 0.016 0.000 0.984 0.000 0.000
#&gt; SRR1975459     2  0.4256     0.3289 0.000 0.564 0.000 0.000 0.436
#&gt; SRR1975460     2  0.4256     0.3289 0.000 0.564 0.000 0.000 0.436
#&gt; SRR1975457     3  0.2690     0.8516 0.000 0.156 0.844 0.000 0.000
#&gt; SRR1975458     3  0.2690     0.8516 0.000 0.156 0.844 0.000 0.000
#&gt; SRR1975455     3  0.2690     0.8516 0.000 0.156 0.844 0.000 0.000
#&gt; SRR1975456     3  0.2690     0.8516 0.000 0.156 0.844 0.000 0.000
#&gt; SRR1975453     3  0.0510     0.9225 0.016 0.000 0.984 0.000 0.000
#&gt; SRR1975454     3  0.0510     0.9225 0.016 0.000 0.984 0.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-4-a').click(function(){
  $('#tab-SD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-5'>
<p><a id='tab-SD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     3  0.0000      0.918 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975507     3  0.0000      0.918 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975506     3  0.0000      0.918 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975505     3  0.0000      0.918 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975503     4  0.5501      0.521 0.000 0.408 0.000 0.504 0.040 0.048
#&gt; SRR1975504     4  0.5501      0.521 0.000 0.408 0.000 0.504 0.040 0.048
#&gt; SRR1975501     6  0.3221      0.823 0.188 0.020 0.000 0.000 0.000 0.792
#&gt; SRR1975502     6  0.3221      0.823 0.188 0.020 0.000 0.000 0.000 0.792
#&gt; SRR1975499     4  0.3514      0.801 0.000 0.080 0.000 0.832 0.040 0.048
#&gt; SRR1975500     4  0.3514      0.801 0.000 0.080 0.000 0.832 0.040 0.048
#&gt; SRR1975497     1  0.0520      0.985 0.984 0.000 0.000 0.000 0.008 0.008
#&gt; SRR1975498     1  0.0520      0.985 0.984 0.000 0.000 0.000 0.008 0.008
#&gt; SRR1975493     2  0.3984      0.859 0.000 0.596 0.000 0.000 0.396 0.008
#&gt; SRR1975494     2  0.3984      0.859 0.000 0.596 0.000 0.000 0.396 0.008
#&gt; SRR1975495     1  0.0000      0.996 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.996 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975491     6  0.2697      0.817 0.000 0.188 0.000 0.000 0.000 0.812
#&gt; SRR1975492     6  0.2697      0.817 0.000 0.188 0.000 0.000 0.000 0.812
#&gt; SRR1975489     4  0.0858      0.842 0.000 0.000 0.000 0.968 0.028 0.004
#&gt; SRR1975490     4  0.0858      0.842 0.000 0.000 0.000 0.968 0.028 0.004
#&gt; SRR1975487     4  0.0000      0.851 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975488     4  0.0000      0.851 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975485     4  0.0146      0.851 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975486     4  0.0146      0.851 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975483     1  0.0000      0.996 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.996 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.996 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.996 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975477     5  0.3370      0.338 0.000 0.148 0.048 0.000 0.804 0.000
#&gt; SRR1975478     5  0.3370      0.338 0.000 0.148 0.048 0.000 0.804 0.000
#&gt; SRR1975479     5  0.6157      0.520 0.000 0.228 0.000 0.072 0.576 0.124
#&gt; SRR1975480     5  0.6157      0.520 0.000 0.228 0.000 0.072 0.576 0.124
#&gt; SRR1975475     5  0.6163      0.542 0.000 0.260 0.000 0.060 0.556 0.124
#&gt; SRR1975476     5  0.6163      0.542 0.000 0.260 0.000 0.060 0.556 0.124
#&gt; SRR1975473     5  0.3370      0.338 0.000 0.148 0.048 0.000 0.804 0.000
#&gt; SRR1975474     5  0.3370      0.338 0.000 0.148 0.048 0.000 0.804 0.000
#&gt; SRR1975471     1  0.0000      0.996 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.996 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975469     1  0.0146      0.994 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1975470     1  0.0146      0.994 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1975467     2  0.0146      0.370 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1975468     2  0.0146      0.370 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1975465     2  0.3984      0.859 0.000 0.596 0.000 0.000 0.396 0.008
#&gt; SRR1975466     2  0.3984      0.859 0.000 0.596 0.000 0.000 0.396 0.008
#&gt; SRR1975463     2  0.3984      0.859 0.000 0.596 0.000 0.000 0.396 0.008
#&gt; SRR1975464     2  0.3984      0.859 0.000 0.596 0.000 0.000 0.396 0.008
#&gt; SRR1975461     3  0.0603      0.913 0.016 0.000 0.980 0.000 0.000 0.004
#&gt; SRR1975462     3  0.0603      0.913 0.016 0.000 0.980 0.000 0.000 0.004
#&gt; SRR1975459     2  0.3984      0.859 0.000 0.596 0.000 0.000 0.396 0.008
#&gt; SRR1975460     2  0.3984      0.859 0.000 0.596 0.000 0.000 0.396 0.008
#&gt; SRR1975457     3  0.2416      0.842 0.000 0.000 0.844 0.000 0.156 0.000
#&gt; SRR1975458     3  0.2416      0.842 0.000 0.000 0.844 0.000 0.156 0.000
#&gt; SRR1975455     3  0.2416      0.842 0.000 0.000 0.844 0.000 0.156 0.000
#&gt; SRR1975456     3  0.2416      0.842 0.000 0.000 0.844 0.000 0.156 0.000
#&gt; SRR1975453     3  0.0603      0.913 0.016 0.000 0.980 0.000 0.000 0.004
#&gt; SRR1975454     3  0.0603      0.913 0.016 0.000 0.980 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-5-a').click(function(){
  $('#tab-SD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-hclust-signature_compare](figure_cola/SD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-hclust-collect-classes](figure_cola/SD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "kmeans"]
# you can also extract it by
# res = res_list["SD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-kmeans-collect-plots](figure_cola/SD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-kmeans-select-partition-number](figure_cola/SD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.399           0.747       0.873         0.4679 0.556   0.556
#> 3 3 0.505           0.642       0.784         0.3956 0.730   0.532
#> 4 4 0.584           0.823       0.814         0.1251 0.865   0.615
#> 5 5 0.665           0.745       0.779         0.0608 1.000   1.000
#> 6 6 0.712           0.658       0.730         0.0440 0.974   0.891
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-classes'>
<ul>
<li><a href='#tab-SD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-kmeans-get-classes-1'>
<p><a id='tab-SD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975507     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975506     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975505     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975503     1  0.1184      0.918 0.984 0.016
#&gt; SRR1975504     1  0.1184      0.918 0.984 0.016
#&gt; SRR1975501     2  0.9896      0.303 0.440 0.560
#&gt; SRR1975502     2  0.9896      0.303 0.440 0.560
#&gt; SRR1975499     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975500     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975497     2  0.9970      0.181 0.468 0.532
#&gt; SRR1975498     2  0.9970      0.181 0.468 0.532
#&gt; SRR1975493     2  0.9754      0.433 0.408 0.592
#&gt; SRR1975494     2  0.9754      0.433 0.408 0.592
#&gt; SRR1975495     2  0.2948      0.804 0.052 0.948
#&gt; SRR1975496     2  0.2948      0.804 0.052 0.948
#&gt; SRR1975491     1  0.9248      0.308 0.660 0.340
#&gt; SRR1975492     1  0.9248      0.308 0.660 0.340
#&gt; SRR1975489     1  0.0376      0.919 0.996 0.004
#&gt; SRR1975490     1  0.0376      0.919 0.996 0.004
#&gt; SRR1975487     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975488     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975485     1  0.0376      0.919 0.996 0.004
#&gt; SRR1975486     1  0.0376      0.919 0.996 0.004
#&gt; SRR1975483     2  0.5294      0.773 0.120 0.880
#&gt; SRR1975484     2  0.5294      0.773 0.120 0.880
#&gt; SRR1975481     2  0.5294      0.773 0.120 0.880
#&gt; SRR1975482     2  0.5294      0.773 0.120 0.880
#&gt; SRR1975477     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975478     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975479     1  0.1414      0.917 0.980 0.020
#&gt; SRR1975480     1  0.1414      0.917 0.980 0.020
#&gt; SRR1975475     1  0.1414      0.917 0.980 0.020
#&gt; SRR1975476     1  0.1414      0.917 0.980 0.020
#&gt; SRR1975473     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975474     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975471     2  0.1414      0.808 0.020 0.980
#&gt; SRR1975472     2  0.1414      0.808 0.020 0.980
#&gt; SRR1975469     2  0.8661      0.593 0.288 0.712
#&gt; SRR1975470     2  0.8661      0.593 0.288 0.712
#&gt; SRR1975467     1  0.5178      0.821 0.884 0.116
#&gt; SRR1975468     1  0.5178      0.821 0.884 0.116
#&gt; SRR1975465     2  0.8267      0.688 0.260 0.740
#&gt; SRR1975466     2  0.8267      0.688 0.260 0.740
#&gt; SRR1975463     2  0.8267      0.688 0.260 0.740
#&gt; SRR1975464     2  0.8267      0.688 0.260 0.740
#&gt; SRR1975461     2  0.0000      0.810 0.000 1.000
#&gt; SRR1975462     2  0.0000      0.810 0.000 1.000
#&gt; SRR1975459     2  0.6712      0.766 0.176 0.824
#&gt; SRR1975460     2  0.6712      0.766 0.176 0.824
#&gt; SRR1975457     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975458     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975455     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975456     2  0.3584      0.824 0.068 0.932
#&gt; SRR1975453     2  0.1184      0.808 0.016 0.984
#&gt; SRR1975454     2  0.1184      0.808 0.016 0.984
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-1-a').click(function(){
  $('#tab-SD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-2'>
<p><a id='tab-SD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     2  0.2939     0.5931 0.072 0.916 0.012
#&gt; SRR1975507     2  0.2939     0.5931 0.072 0.916 0.012
#&gt; SRR1975506     2  0.2939     0.5931 0.072 0.916 0.012
#&gt; SRR1975505     2  0.2939     0.5931 0.072 0.916 0.012
#&gt; SRR1975503     3  0.2590     0.8561 0.072 0.004 0.924
#&gt; SRR1975504     3  0.2590     0.8561 0.072 0.004 0.924
#&gt; SRR1975501     1  0.4092     0.5158 0.876 0.036 0.088
#&gt; SRR1975502     1  0.4092     0.5158 0.876 0.036 0.088
#&gt; SRR1975499     3  0.0237     0.8832 0.004 0.000 0.996
#&gt; SRR1975500     3  0.0237     0.8832 0.004 0.000 0.996
#&gt; SRR1975497     1  0.8297     0.6776 0.632 0.200 0.168
#&gt; SRR1975498     1  0.8297     0.6776 0.632 0.200 0.168
#&gt; SRR1975493     2  0.8871     0.4803 0.408 0.472 0.120
#&gt; SRR1975494     2  0.8871     0.4803 0.408 0.472 0.120
#&gt; SRR1975495     1  0.7065     0.7429 0.616 0.352 0.032
#&gt; SRR1975496     1  0.7065     0.7429 0.616 0.352 0.032
#&gt; SRR1975491     1  0.8351     0.0406 0.604 0.124 0.272
#&gt; SRR1975492     1  0.8351     0.0406 0.604 0.124 0.272
#&gt; SRR1975489     3  0.1170     0.8825 0.016 0.008 0.976
#&gt; SRR1975490     3  0.1170     0.8825 0.016 0.008 0.976
#&gt; SRR1975487     3  0.0848     0.8836 0.008 0.008 0.984
#&gt; SRR1975488     3  0.0848     0.8836 0.008 0.008 0.984
#&gt; SRR1975485     3  0.1170     0.8818 0.016 0.008 0.976
#&gt; SRR1975486     3  0.1170     0.8818 0.016 0.008 0.976
#&gt; SRR1975483     1  0.7065     0.7429 0.616 0.352 0.032
#&gt; SRR1975484     1  0.7065     0.7429 0.616 0.352 0.032
#&gt; SRR1975481     1  0.7023     0.7434 0.624 0.344 0.032
#&gt; SRR1975482     1  0.7023     0.7434 0.624 0.344 0.032
#&gt; SRR1975477     2  0.2269     0.6479 0.040 0.944 0.016
#&gt; SRR1975478     2  0.2269     0.6479 0.040 0.944 0.016
#&gt; SRR1975479     3  0.2773     0.8725 0.024 0.048 0.928
#&gt; SRR1975480     3  0.2773     0.8725 0.024 0.048 0.928
#&gt; SRR1975475     3  0.2918     0.8719 0.032 0.044 0.924
#&gt; SRR1975476     3  0.2918     0.8719 0.032 0.044 0.924
#&gt; SRR1975473     2  0.2804     0.6468 0.060 0.924 0.016
#&gt; SRR1975474     2  0.2804     0.6468 0.060 0.924 0.016
#&gt; SRR1975471     1  0.6154     0.6930 0.592 0.408 0.000
#&gt; SRR1975472     1  0.6154     0.6930 0.592 0.408 0.000
#&gt; SRR1975469     1  0.7911     0.7247 0.632 0.272 0.096
#&gt; SRR1975470     1  0.7911     0.7247 0.632 0.272 0.096
#&gt; SRR1975467     3  0.9713     0.1324 0.376 0.220 0.404
#&gt; SRR1975468     3  0.9713     0.1324 0.376 0.220 0.404
#&gt; SRR1975465     2  0.8373     0.5299 0.388 0.524 0.088
#&gt; SRR1975466     2  0.8373     0.5299 0.388 0.524 0.088
#&gt; SRR1975463     2  0.8373     0.5299 0.388 0.524 0.088
#&gt; SRR1975464     2  0.8373     0.5299 0.388 0.524 0.088
#&gt; SRR1975461     2  0.4452     0.3751 0.192 0.808 0.000
#&gt; SRR1975462     2  0.4452     0.3751 0.192 0.808 0.000
#&gt; SRR1975459     2  0.8373     0.5299 0.388 0.524 0.088
#&gt; SRR1975460     2  0.8373     0.5299 0.388 0.524 0.088
#&gt; SRR1975457     2  0.1482     0.6346 0.020 0.968 0.012
#&gt; SRR1975458     2  0.1482     0.6346 0.020 0.968 0.012
#&gt; SRR1975455     2  0.1482     0.6346 0.020 0.968 0.012
#&gt; SRR1975456     2  0.1482     0.6346 0.020 0.968 0.012
#&gt; SRR1975453     1  0.6260     0.6377 0.552 0.448 0.000
#&gt; SRR1975454     1  0.6260     0.6377 0.552 0.448 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-2-a').click(function(){
  $('#tab-SD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-3'>
<p><a id='tab-SD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3   0.259      0.855 0.116 0.000 0.884 0.000
#&gt; SRR1975507     3   0.259      0.855 0.116 0.000 0.884 0.000
#&gt; SRR1975506     3   0.259      0.855 0.116 0.000 0.884 0.000
#&gt; SRR1975505     3   0.259      0.855 0.116 0.000 0.884 0.000
#&gt; SRR1975503     4   0.526      0.769 0.016 0.224 0.028 0.732
#&gt; SRR1975504     4   0.526      0.769 0.016 0.224 0.028 0.732
#&gt; SRR1975501     1   0.462      0.700 0.760 0.216 0.004 0.020
#&gt; SRR1975502     1   0.462      0.700 0.760 0.216 0.004 0.020
#&gt; SRR1975499     4   0.257      0.885 0.004 0.052 0.028 0.916
#&gt; SRR1975500     4   0.257      0.885 0.004 0.052 0.028 0.916
#&gt; SRR1975497     1   0.333      0.815 0.884 0.064 0.008 0.044
#&gt; SRR1975498     1   0.333      0.815 0.884 0.064 0.008 0.044
#&gt; SRR1975493     2   0.501      0.849 0.024 0.772 0.176 0.028
#&gt; SRR1975494     2   0.501      0.849 0.024 0.772 0.176 0.028
#&gt; SRR1975495     1   0.288      0.876 0.900 0.028 0.068 0.004
#&gt; SRR1975496     1   0.288      0.876 0.900 0.028 0.068 0.004
#&gt; SRR1975491     2   0.569      0.691 0.160 0.748 0.032 0.060
#&gt; SRR1975492     2   0.569      0.691 0.160 0.748 0.032 0.060
#&gt; SRR1975489     4   0.228      0.889 0.012 0.020 0.036 0.932
#&gt; SRR1975490     4   0.228      0.889 0.012 0.020 0.036 0.932
#&gt; SRR1975487     4   0.117      0.891 0.000 0.020 0.012 0.968
#&gt; SRR1975488     4   0.117      0.891 0.000 0.020 0.012 0.968
#&gt; SRR1975485     4   0.139      0.891 0.012 0.016 0.008 0.964
#&gt; SRR1975486     4   0.139      0.891 0.012 0.016 0.008 0.964
#&gt; SRR1975483     1   0.271      0.878 0.908 0.024 0.064 0.004
#&gt; SRR1975484     1   0.271      0.878 0.908 0.024 0.064 0.004
#&gt; SRR1975481     1   0.300      0.878 0.896 0.036 0.064 0.004
#&gt; SRR1975482     1   0.300      0.878 0.896 0.036 0.064 0.004
#&gt; SRR1975477     3   0.534      0.767 0.072 0.180 0.744 0.004
#&gt; SRR1975478     3   0.534      0.767 0.072 0.180 0.744 0.004
#&gt; SRR1975479     4   0.511      0.854 0.028 0.096 0.080 0.796
#&gt; SRR1975480     4   0.511      0.854 0.028 0.096 0.080 0.796
#&gt; SRR1975475     4   0.547      0.848 0.028 0.112 0.088 0.772
#&gt; SRR1975476     4   0.547      0.848 0.028 0.112 0.088 0.772
#&gt; SRR1975473     3   0.536      0.741 0.064 0.196 0.736 0.004
#&gt; SRR1975474     3   0.536      0.741 0.064 0.196 0.736 0.004
#&gt; SRR1975471     1   0.318      0.861 0.880 0.036 0.084 0.000
#&gt; SRR1975472     1   0.318      0.861 0.880 0.036 0.084 0.000
#&gt; SRR1975469     1   0.350      0.872 0.880 0.048 0.056 0.016
#&gt; SRR1975470     1   0.350      0.872 0.880 0.048 0.056 0.016
#&gt; SRR1975467     2   0.505      0.736 0.008 0.780 0.076 0.136
#&gt; SRR1975468     2   0.505      0.736 0.008 0.780 0.076 0.136
#&gt; SRR1975465     2   0.537      0.850 0.020 0.728 0.224 0.028
#&gt; SRR1975466     2   0.537      0.850 0.020 0.728 0.224 0.028
#&gt; SRR1975463     2   0.537      0.850 0.020 0.728 0.224 0.028
#&gt; SRR1975464     2   0.537      0.850 0.020 0.728 0.224 0.028
#&gt; SRR1975461     3   0.436      0.766 0.188 0.028 0.784 0.000
#&gt; SRR1975462     3   0.436      0.766 0.188 0.028 0.784 0.000
#&gt; SRR1975459     2   0.531      0.843 0.024 0.728 0.228 0.020
#&gt; SRR1975460     2   0.531      0.843 0.024 0.728 0.228 0.020
#&gt; SRR1975457     3   0.392      0.863 0.104 0.056 0.840 0.000
#&gt; SRR1975458     3   0.392      0.863 0.104 0.056 0.840 0.000
#&gt; SRR1975455     3   0.414      0.861 0.104 0.068 0.828 0.000
#&gt; SRR1975456     3   0.414      0.861 0.104 0.068 0.828 0.000
#&gt; SRR1975453     1   0.518      0.614 0.684 0.028 0.288 0.000
#&gt; SRR1975454     1   0.518      0.614 0.684 0.028 0.288 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-3-a').click(function(){
  $('#tab-SD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-4'>
<p><a id='tab-SD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR1975508     3  0.0703      0.789 0.024 0.000 0.976 0.000 NA
#&gt; SRR1975507     3  0.0703      0.789 0.024 0.000 0.976 0.000 NA
#&gt; SRR1975506     3  0.0703      0.789 0.024 0.000 0.976 0.000 NA
#&gt; SRR1975505     3  0.0703      0.789 0.024 0.000 0.976 0.000 NA
#&gt; SRR1975503     4  0.6521      0.594 0.000 0.216 0.008 0.532 NA
#&gt; SRR1975504     4  0.6521      0.594 0.000 0.216 0.008 0.532 NA
#&gt; SRR1975501     1  0.5227      0.690 0.696 0.132 0.004 0.000 NA
#&gt; SRR1975502     1  0.5227      0.690 0.696 0.132 0.004 0.000 NA
#&gt; SRR1975499     4  0.3646      0.778 0.008 0.032 0.000 0.820 NA
#&gt; SRR1975500     4  0.3646      0.778 0.008 0.032 0.000 0.820 NA
#&gt; SRR1975497     1  0.4404      0.759 0.788 0.032 0.008 0.024 NA
#&gt; SRR1975498     1  0.4404      0.759 0.788 0.032 0.008 0.024 NA
#&gt; SRR1975493     2  0.3355      0.809 0.004 0.860 0.076 0.008 NA
#&gt; SRR1975494     2  0.3355      0.809 0.004 0.860 0.076 0.008 NA
#&gt; SRR1975495     1  0.2206      0.837 0.912 0.004 0.068 0.000 NA
#&gt; SRR1975496     1  0.2206      0.837 0.912 0.004 0.068 0.000 NA
#&gt; SRR1975491     2  0.5819      0.585 0.104 0.676 0.004 0.028 NA
#&gt; SRR1975492     2  0.5819      0.585 0.104 0.676 0.004 0.028 NA
#&gt; SRR1975489     4  0.2361      0.797 0.000 0.012 0.000 0.892 NA
#&gt; SRR1975490     4  0.2361      0.797 0.000 0.012 0.000 0.892 NA
#&gt; SRR1975487     4  0.1195      0.798 0.000 0.012 0.000 0.960 NA
#&gt; SRR1975488     4  0.1195      0.798 0.000 0.012 0.000 0.960 NA
#&gt; SRR1975485     4  0.2100      0.797 0.012 0.016 0.000 0.924 NA
#&gt; SRR1975486     4  0.2100      0.797 0.012 0.016 0.000 0.924 NA
#&gt; SRR1975483     1  0.2166      0.838 0.912 0.004 0.072 0.000 NA
#&gt; SRR1975484     1  0.2166      0.838 0.912 0.004 0.072 0.000 NA
#&gt; SRR1975481     1  0.3356      0.833 0.860 0.016 0.068 0.000 NA
#&gt; SRR1975482     1  0.3356      0.833 0.860 0.016 0.068 0.000 NA
#&gt; SRR1975477     3  0.6445      0.675 0.024 0.188 0.616 0.008 NA
#&gt; SRR1975478     3  0.6445      0.675 0.024 0.188 0.616 0.008 NA
#&gt; SRR1975479     4  0.5881      0.702 0.016 0.052 0.012 0.596 NA
#&gt; SRR1975480     4  0.5881      0.702 0.016 0.052 0.012 0.596 NA
#&gt; SRR1975475     4  0.6535      0.690 0.024 0.088 0.012 0.548 NA
#&gt; SRR1975476     4  0.6535      0.690 0.024 0.088 0.012 0.548 NA
#&gt; SRR1975473     3  0.6621      0.623 0.016 0.212 0.576 0.008 NA
#&gt; SRR1975474     3  0.6621      0.623 0.016 0.212 0.576 0.008 NA
#&gt; SRR1975471     1  0.2959      0.819 0.864 0.000 0.100 0.000 NA
#&gt; SRR1975472     1  0.2959      0.819 0.864 0.000 0.100 0.000 NA
#&gt; SRR1975469     1  0.4372      0.814 0.792 0.008 0.068 0.008 NA
#&gt; SRR1975470     1  0.4372      0.814 0.792 0.008 0.068 0.008 NA
#&gt; SRR1975467     2  0.4605      0.720 0.004 0.780 0.028 0.052 NA
#&gt; SRR1975468     2  0.4605      0.720 0.004 0.780 0.028 0.052 NA
#&gt; SRR1975465     2  0.3409      0.813 0.004 0.824 0.156 0.008 NA
#&gt; SRR1975466     2  0.3409      0.813 0.004 0.824 0.156 0.008 NA
#&gt; SRR1975463     2  0.3129      0.813 0.004 0.832 0.156 0.008 NA
#&gt; SRR1975464     2  0.3129      0.813 0.004 0.832 0.156 0.008 NA
#&gt; SRR1975461     3  0.3767      0.669 0.120 0.000 0.812 0.000 NA
#&gt; SRR1975462     3  0.3767      0.669 0.120 0.000 0.812 0.000 NA
#&gt; SRR1975459     2  0.3409      0.813 0.004 0.824 0.156 0.008 NA
#&gt; SRR1975460     2  0.3409      0.813 0.004 0.824 0.156 0.008 NA
#&gt; SRR1975457     3  0.3942      0.800 0.020 0.068 0.824 0.000 NA
#&gt; SRR1975458     3  0.3942      0.800 0.020 0.068 0.824 0.000 NA
#&gt; SRR1975455     3  0.4164      0.798 0.020 0.072 0.808 0.000 NA
#&gt; SRR1975456     3  0.4164      0.798 0.020 0.072 0.808 0.000 NA
#&gt; SRR1975453     1  0.5432      0.409 0.544 0.000 0.392 0.000 NA
#&gt; SRR1975454     1  0.5432      0.409 0.544 0.000 0.392 0.000 NA
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-4-a').click(function(){
  $('#tab-SD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-5'>
<p><a id='tab-SD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5    p6
#&gt; SRR1975508     5  0.1218     0.7193 0.028 0.012 NA 0.000 0.956 0.004
#&gt; SRR1975507     5  0.1218     0.7193 0.028 0.012 NA 0.000 0.956 0.004
#&gt; SRR1975506     5  0.1332     0.7193 0.028 0.012 NA 0.000 0.952 0.008
#&gt; SRR1975505     5  0.1332     0.7193 0.028 0.012 NA 0.000 0.952 0.008
#&gt; SRR1975503     4  0.6972     0.0735 0.000 0.156 NA 0.484 0.004 0.248
#&gt; SRR1975504     4  0.6972     0.0735 0.000 0.156 NA 0.484 0.004 0.248
#&gt; SRR1975501     1  0.5317     0.5964 0.564 0.096 NA 0.000 0.000 0.008
#&gt; SRR1975502     1  0.5317     0.5964 0.564 0.096 NA 0.000 0.000 0.008
#&gt; SRR1975499     4  0.3487     0.5546 0.004 0.004 NA 0.828 0.004 0.092
#&gt; SRR1975500     4  0.3487     0.5546 0.004 0.004 NA 0.828 0.004 0.092
#&gt; SRR1975497     1  0.4739     0.6357 0.592 0.004 NA 0.008 0.000 0.032
#&gt; SRR1975498     1  0.4739     0.6357 0.592 0.004 NA 0.008 0.000 0.032
#&gt; SRR1975493     2  0.3021     0.7906 0.000 0.860 NA 0.000 0.020 0.044
#&gt; SRR1975494     2  0.3021     0.7906 0.000 0.860 NA 0.000 0.020 0.044
#&gt; SRR1975495     1  0.2537     0.7640 0.880 0.000 NA 0.000 0.024 0.008
#&gt; SRR1975496     1  0.2537     0.7640 0.880 0.000 NA 0.000 0.024 0.008
#&gt; SRR1975491     2  0.6555     0.5353 0.072 0.508 NA 0.008 0.000 0.108
#&gt; SRR1975492     2  0.6555     0.5353 0.072 0.508 NA 0.008 0.000 0.108
#&gt; SRR1975489     4  0.3649     0.4905 0.004 0.000 NA 0.800 0.000 0.112
#&gt; SRR1975490     4  0.3739     0.4905 0.004 0.000 NA 0.800 0.004 0.112
#&gt; SRR1975487     4  0.0696     0.6182 0.004 0.000 NA 0.980 0.004 0.008
#&gt; SRR1975488     4  0.0696     0.6182 0.004 0.000 NA 0.980 0.004 0.008
#&gt; SRR1975485     4  0.2487     0.5785 0.004 0.000 NA 0.892 0.004 0.052
#&gt; SRR1975486     4  0.2487     0.5785 0.004 0.000 NA 0.892 0.004 0.052
#&gt; SRR1975483     1  0.2408     0.7680 0.896 0.004 NA 0.000 0.024 0.008
#&gt; SRR1975484     1  0.2408     0.7680 0.896 0.004 NA 0.000 0.024 0.008
#&gt; SRR1975481     1  0.3944     0.7472 0.800 0.004 NA 0.000 0.020 0.088
#&gt; SRR1975482     1  0.3944     0.7472 0.800 0.004 NA 0.000 0.020 0.088
#&gt; SRR1975477     5  0.6648     0.6715 0.020 0.168 NA 0.000 0.524 0.248
#&gt; SRR1975478     5  0.6648     0.6715 0.020 0.168 NA 0.000 0.524 0.248
#&gt; SRR1975479     6  0.6023     0.7349 0.004 0.028 NA 0.392 0.024 0.500
#&gt; SRR1975480     6  0.6023     0.7349 0.004 0.028 NA 0.392 0.024 0.500
#&gt; SRR1975475     6  0.5536     0.7294 0.000 0.036 NA 0.364 0.016 0.552
#&gt; SRR1975476     6  0.5536     0.7294 0.000 0.036 NA 0.364 0.016 0.552
#&gt; SRR1975473     5  0.6857     0.6408 0.016 0.176 NA 0.000 0.488 0.268
#&gt; SRR1975474     5  0.6857     0.6408 0.016 0.176 NA 0.000 0.488 0.268
#&gt; SRR1975471     1  0.3432     0.7341 0.836 0.000 NA 0.000 0.044 0.036
#&gt; SRR1975472     1  0.3432     0.7341 0.836 0.000 NA 0.000 0.044 0.036
#&gt; SRR1975469     1  0.4677     0.7248 0.736 0.008 NA 0.000 0.016 0.108
#&gt; SRR1975470     1  0.4677     0.7248 0.736 0.008 NA 0.000 0.016 0.108
#&gt; SRR1975467     2  0.5215     0.6379 0.000 0.668 NA 0.028 0.004 0.212
#&gt; SRR1975468     2  0.5215     0.6379 0.000 0.668 NA 0.028 0.004 0.212
#&gt; SRR1975465     2  0.1429     0.8155 0.000 0.940 NA 0.000 0.052 0.004
#&gt; SRR1975466     2  0.1429     0.8155 0.000 0.940 NA 0.000 0.052 0.004
#&gt; SRR1975463     2  0.1757     0.8140 0.000 0.928 NA 0.000 0.052 0.008
#&gt; SRR1975464     2  0.1757     0.8140 0.000 0.928 NA 0.000 0.052 0.008
#&gt; SRR1975461     5  0.4536     0.5470 0.140 0.000 NA 0.000 0.748 0.044
#&gt; SRR1975462     5  0.4536     0.5470 0.140 0.000 NA 0.000 0.748 0.044
#&gt; SRR1975459     2  0.1757     0.8132 0.000 0.928 NA 0.000 0.052 0.008
#&gt; SRR1975460     2  0.1757     0.8132 0.000 0.928 NA 0.000 0.052 0.008
#&gt; SRR1975457     5  0.5115     0.7543 0.024 0.080 NA 0.000 0.724 0.136
#&gt; SRR1975458     5  0.5115     0.7543 0.024 0.080 NA 0.000 0.724 0.136
#&gt; SRR1975455     5  0.5666     0.7458 0.028 0.092 NA 0.000 0.672 0.168
#&gt; SRR1975456     5  0.5666     0.7458 0.028 0.092 NA 0.000 0.672 0.168
#&gt; SRR1975453     1  0.5733     0.4718 0.580 0.000 NA 0.000 0.284 0.040
#&gt; SRR1975454     1  0.5733     0.4718 0.580 0.000 NA 0.000 0.284 0.040
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-5-a').click(function(){
  $('#tab-SD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-kmeans-signature_compare](figure_cola/SD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-kmeans-collect-classes](figure_cola/SD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "skmeans"]
# you can also extract it by
# res = res_list["SD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-skmeans-collect-plots](figure_cola/SD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-skmeans-select-partition-number](figure_cola/SD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.545           0.576       0.844         0.5085 0.491   0.491
#> 3 3 0.670           0.887       0.911         0.3148 0.758   0.544
#> 4 4 1.000           1.000       1.000         0.1387 0.870   0.627
#> 5 5 0.857           0.717       0.836         0.0537 0.943   0.773
#> 6 6 0.829           0.751       0.835         0.0331 0.938   0.718
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-classes'>
<ul>
<li><a href='#tab-SD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-skmeans-get-classes-1'>
<p><a id='tab-SD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2   0.966      0.809 0.392 0.608
#&gt; SRR1975507     2   0.966      0.809 0.392 0.608
#&gt; SRR1975506     2   0.966      0.809 0.392 0.608
#&gt; SRR1975505     2   0.966      0.809 0.392 0.608
#&gt; SRR1975503     1   0.966      0.783 0.608 0.392
#&gt; SRR1975504     1   0.966      0.783 0.608 0.392
#&gt; SRR1975501     1   0.966      0.783 0.608 0.392
#&gt; SRR1975502     1   0.966      0.783 0.608 0.392
#&gt; SRR1975499     1   0.966      0.783 0.608 0.392
#&gt; SRR1975500     1   0.966      0.783 0.608 0.392
#&gt; SRR1975497     1   0.000      0.348 1.000 0.000
#&gt; SRR1975498     1   0.000      0.348 1.000 0.000
#&gt; SRR1975493     2   0.973     -0.547 0.404 0.596
#&gt; SRR1975494     2   0.973     -0.547 0.404 0.596
#&gt; SRR1975495     2   0.966      0.809 0.392 0.608
#&gt; SRR1975496     2   0.966      0.809 0.392 0.608
#&gt; SRR1975491     1   0.966      0.783 0.608 0.392
#&gt; SRR1975492     1   0.966      0.783 0.608 0.392
#&gt; SRR1975489     1   0.966      0.783 0.608 0.392
#&gt; SRR1975490     1   0.966      0.783 0.608 0.392
#&gt; SRR1975487     1   0.966      0.783 0.608 0.392
#&gt; SRR1975488     1   0.966      0.783 0.608 0.392
#&gt; SRR1975485     1   0.966      0.783 0.608 0.392
#&gt; SRR1975486     1   0.966      0.783 0.608 0.392
#&gt; SRR1975483     1   0.975     -0.561 0.592 0.408
#&gt; SRR1975484     1   0.975     -0.561 0.592 0.408
#&gt; SRR1975481     1   0.975     -0.561 0.592 0.408
#&gt; SRR1975482     1   0.975     -0.561 0.592 0.408
#&gt; SRR1975477     2   0.966      0.809 0.392 0.608
#&gt; SRR1975478     2   0.966      0.809 0.392 0.608
#&gt; SRR1975479     1   0.966      0.783 0.608 0.392
#&gt; SRR1975480     1   0.966      0.783 0.608 0.392
#&gt; SRR1975475     1   0.966      0.783 0.608 0.392
#&gt; SRR1975476     1   0.966      0.783 0.608 0.392
#&gt; SRR1975473     2   0.966      0.809 0.392 0.608
#&gt; SRR1975474     2   0.966      0.809 0.392 0.608
#&gt; SRR1975471     2   0.966      0.809 0.392 0.608
#&gt; SRR1975472     2   0.966      0.809 0.392 0.608
#&gt; SRR1975469     1   0.000      0.348 1.000 0.000
#&gt; SRR1975470     1   0.000      0.348 1.000 0.000
#&gt; SRR1975467     1   0.966      0.783 0.608 0.392
#&gt; SRR1975468     1   0.966      0.783 0.608 0.392
#&gt; SRR1975465     2   0.000      0.396 0.000 1.000
#&gt; SRR1975466     2   0.000      0.396 0.000 1.000
#&gt; SRR1975463     2   0.000      0.396 0.000 1.000
#&gt; SRR1975464     2   0.000      0.396 0.000 1.000
#&gt; SRR1975461     2   0.966      0.809 0.392 0.608
#&gt; SRR1975462     2   0.966      0.809 0.392 0.608
#&gt; SRR1975459     2   0.000      0.396 0.000 1.000
#&gt; SRR1975460     2   0.000      0.396 0.000 1.000
#&gt; SRR1975457     2   0.966      0.809 0.392 0.608
#&gt; SRR1975458     2   0.966      0.809 0.392 0.608
#&gt; SRR1975455     2   0.966      0.809 0.392 0.608
#&gt; SRR1975456     2   0.966      0.809 0.392 0.608
#&gt; SRR1975453     2   0.966      0.809 0.392 0.608
#&gt; SRR1975454     2   0.966      0.809 0.392 0.608
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-1-a').click(function(){
  $('#tab-SD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-2'>
<p><a id='tab-SD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975507     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975506     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975505     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975503     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975504     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975501     1  0.0424      0.852 0.992 0.000 0.008
#&gt; SRR1975502     1  0.0424      0.852 0.992 0.000 0.008
#&gt; SRR1975499     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975500     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975497     1  0.4475      0.927 0.864 0.072 0.064
#&gt; SRR1975498     1  0.4475      0.927 0.864 0.072 0.064
#&gt; SRR1975493     2  0.8460      0.589 0.136 0.600 0.264
#&gt; SRR1975494     2  0.8460      0.589 0.136 0.600 0.264
#&gt; SRR1975495     1  0.3619      0.955 0.864 0.136 0.000
#&gt; SRR1975496     1  0.3619      0.955 0.864 0.136 0.000
#&gt; SRR1975491     3  0.3619      0.881 0.136 0.000 0.864
#&gt; SRR1975492     3  0.3619      0.881 0.136 0.000 0.864
#&gt; SRR1975489     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975490     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975487     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975488     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975485     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975486     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975483     1  0.3619      0.955 0.864 0.136 0.000
#&gt; SRR1975484     1  0.3619      0.955 0.864 0.136 0.000
#&gt; SRR1975481     1  0.3619      0.955 0.864 0.136 0.000
#&gt; SRR1975482     1  0.3619      0.955 0.864 0.136 0.000
#&gt; SRR1975477     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975478     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975479     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975480     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975475     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975476     3  0.0000      0.968 0.000 0.000 1.000
#&gt; SRR1975473     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975474     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975471     1  0.3619      0.955 0.864 0.136 0.000
#&gt; SRR1975472     1  0.3619      0.955 0.864 0.136 0.000
#&gt; SRR1975469     1  0.4475      0.921 0.864 0.064 0.072
#&gt; SRR1975470     1  0.4475      0.921 0.864 0.064 0.072
#&gt; SRR1975467     3  0.3619      0.881 0.136 0.000 0.864
#&gt; SRR1975468     3  0.3619      0.881 0.136 0.000 0.864
#&gt; SRR1975465     2  0.6788      0.778 0.136 0.744 0.120
#&gt; SRR1975466     2  0.6788      0.778 0.136 0.744 0.120
#&gt; SRR1975463     2  0.6788      0.778 0.136 0.744 0.120
#&gt; SRR1975464     2  0.6788      0.778 0.136 0.744 0.120
#&gt; SRR1975461     2  0.3686      0.720 0.140 0.860 0.000
#&gt; SRR1975462     2  0.3686      0.720 0.140 0.860 0.000
#&gt; SRR1975459     2  0.6788      0.778 0.136 0.744 0.120
#&gt; SRR1975460     2  0.6788      0.778 0.136 0.744 0.120
#&gt; SRR1975457     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975458     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975455     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975456     2  0.0000      0.862 0.000 1.000 0.000
#&gt; SRR1975453     1  0.3619      0.955 0.864 0.136 0.000
#&gt; SRR1975454     1  0.3619      0.955 0.864 0.136 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-2-a').click(function(){
  $('#tab-SD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-3'>
<p><a id='tab-SD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1975508     3       0          1  0  0  1  0
#&gt; SRR1975507     3       0          1  0  0  1  0
#&gt; SRR1975506     3       0          1  0  0  1  0
#&gt; SRR1975505     3       0          1  0  0  1  0
#&gt; SRR1975503     4       0          1  0  0  0  1
#&gt; SRR1975504     4       0          1  0  0  0  1
#&gt; SRR1975501     1       0          1  1  0  0  0
#&gt; SRR1975502     1       0          1  1  0  0  0
#&gt; SRR1975499     4       0          1  0  0  0  1
#&gt; SRR1975500     4       0          1  0  0  0  1
#&gt; SRR1975497     1       0          1  1  0  0  0
#&gt; SRR1975498     1       0          1  1  0  0  0
#&gt; SRR1975493     2       0          1  0  1  0  0
#&gt; SRR1975494     2       0          1  0  1  0  0
#&gt; SRR1975495     1       0          1  1  0  0  0
#&gt; SRR1975496     1       0          1  1  0  0  0
#&gt; SRR1975491     2       0          1  0  1  0  0
#&gt; SRR1975492     2       0          1  0  1  0  0
#&gt; SRR1975489     4       0          1  0  0  0  1
#&gt; SRR1975490     4       0          1  0  0  0  1
#&gt; SRR1975487     4       0          1  0  0  0  1
#&gt; SRR1975488     4       0          1  0  0  0  1
#&gt; SRR1975485     4       0          1  0  0  0  1
#&gt; SRR1975486     4       0          1  0  0  0  1
#&gt; SRR1975483     1       0          1  1  0  0  0
#&gt; SRR1975484     1       0          1  1  0  0  0
#&gt; SRR1975481     1       0          1  1  0  0  0
#&gt; SRR1975482     1       0          1  1  0  0  0
#&gt; SRR1975477     3       0          1  0  0  1  0
#&gt; SRR1975478     3       0          1  0  0  1  0
#&gt; SRR1975479     4       0          1  0  0  0  1
#&gt; SRR1975480     4       0          1  0  0  0  1
#&gt; SRR1975475     4       0          1  0  0  0  1
#&gt; SRR1975476     4       0          1  0  0  0  1
#&gt; SRR1975473     3       0          1  0  0  1  0
#&gt; SRR1975474     3       0          1  0  0  1  0
#&gt; SRR1975471     1       0          1  1  0  0  0
#&gt; SRR1975472     1       0          1  1  0  0  0
#&gt; SRR1975469     1       0          1  1  0  0  0
#&gt; SRR1975470     1       0          1  1  0  0  0
#&gt; SRR1975467     2       0          1  0  1  0  0
#&gt; SRR1975468     2       0          1  0  1  0  0
#&gt; SRR1975465     2       0          1  0  1  0  0
#&gt; SRR1975466     2       0          1  0  1  0  0
#&gt; SRR1975463     2       0          1  0  1  0  0
#&gt; SRR1975464     2       0          1  0  1  0  0
#&gt; SRR1975461     3       0          1  0  0  1  0
#&gt; SRR1975462     3       0          1  0  0  1  0
#&gt; SRR1975459     2       0          1  0  1  0  0
#&gt; SRR1975460     2       0          1  0  1  0  0
#&gt; SRR1975457     3       0          1  0  0  1  0
#&gt; SRR1975458     3       0          1  0  0  1  0
#&gt; SRR1975455     3       0          1  0  0  1  0
#&gt; SRR1975456     3       0          1  0  0  1  0
#&gt; SRR1975453     1       0          1  1  0  0  0
#&gt; SRR1975454     1       0          1  1  0  0  0
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-3-a').click(function(){
  $('#tab-SD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-4'>
<p><a id='tab-SD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.0000      0.399 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975507     3  0.0000      0.399 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975506     3  0.0000      0.399 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975505     3  0.0000      0.399 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975503     4  0.0794      0.973 0.000 0.000 0.000 0.972 0.028
#&gt; SRR1975504     4  0.0794      0.973 0.000 0.000 0.000 0.972 0.028
#&gt; SRR1975501     1  0.2329      0.809 0.876 0.000 0.000 0.000 0.124
#&gt; SRR1975502     1  0.2329      0.809 0.876 0.000 0.000 0.000 0.124
#&gt; SRR1975499     4  0.0290      0.983 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975500     4  0.0290      0.983 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975497     1  0.1121      0.842 0.956 0.000 0.000 0.000 0.044
#&gt; SRR1975498     1  0.1121      0.842 0.956 0.000 0.000 0.000 0.044
#&gt; SRR1975493     2  0.0290      0.945 0.000 0.992 0.000 0.000 0.008
#&gt; SRR1975494     2  0.0290      0.945 0.000 0.992 0.000 0.000 0.008
#&gt; SRR1975495     1  0.3395      0.833 0.764 0.000 0.000 0.000 0.236
#&gt; SRR1975496     1  0.3395      0.833 0.764 0.000 0.000 0.000 0.236
#&gt; SRR1975491     2  0.5010      0.742 0.144 0.708 0.000 0.000 0.148
#&gt; SRR1975492     2  0.5010      0.742 0.144 0.708 0.000 0.000 0.148
#&gt; SRR1975489     4  0.0000      0.984 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975490     4  0.0000      0.984 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975487     4  0.0000      0.984 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975488     4  0.0000      0.984 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975485     4  0.0000      0.984 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975486     4  0.0000      0.984 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975483     1  0.2929      0.855 0.820 0.000 0.000 0.000 0.180
#&gt; SRR1975484     1  0.2929      0.855 0.820 0.000 0.000 0.000 0.180
#&gt; SRR1975481     1  0.2179      0.864 0.888 0.000 0.000 0.000 0.112
#&gt; SRR1975482     1  0.2179      0.864 0.888 0.000 0.000 0.000 0.112
#&gt; SRR1975477     5  0.4256      1.000 0.000 0.000 0.436 0.000 0.564
#&gt; SRR1975478     5  0.4256      1.000 0.000 0.000 0.436 0.000 0.564
#&gt; SRR1975479     4  0.1608      0.937 0.000 0.000 0.000 0.928 0.072
#&gt; SRR1975480     4  0.1608      0.937 0.000 0.000 0.000 0.928 0.072
#&gt; SRR1975475     4  0.0290      0.983 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975476     4  0.0290      0.983 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975473     5  0.4256      1.000 0.000 0.000 0.436 0.000 0.564
#&gt; SRR1975474     5  0.4256      1.000 0.000 0.000 0.436 0.000 0.564
#&gt; SRR1975471     1  0.4161      0.792 0.704 0.000 0.016 0.000 0.280
#&gt; SRR1975472     1  0.4161      0.792 0.704 0.000 0.016 0.000 0.280
#&gt; SRR1975469     1  0.0963      0.847 0.964 0.000 0.000 0.000 0.036
#&gt; SRR1975470     1  0.0963      0.847 0.964 0.000 0.000 0.000 0.036
#&gt; SRR1975467     2  0.0880      0.937 0.000 0.968 0.000 0.000 0.032
#&gt; SRR1975468     2  0.0880      0.937 0.000 0.968 0.000 0.000 0.032
#&gt; SRR1975465     2  0.0162      0.946 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1975466     2  0.0162      0.946 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1975463     2  0.0162      0.946 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1975464     2  0.0162      0.946 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1975461     3  0.3395      0.434 0.000 0.000 0.764 0.000 0.236
#&gt; SRR1975462     3  0.3395      0.434 0.000 0.000 0.764 0.000 0.236
#&gt; SRR1975459     2  0.0162      0.946 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1975460     2  0.0162      0.946 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1975457     3  0.4256     -0.713 0.000 0.000 0.564 0.000 0.436
#&gt; SRR1975458     3  0.4256     -0.713 0.000 0.000 0.564 0.000 0.436
#&gt; SRR1975455     3  0.4297     -0.787 0.000 0.000 0.528 0.000 0.472
#&gt; SRR1975456     3  0.4297     -0.787 0.000 0.000 0.528 0.000 0.472
#&gt; SRR1975453     3  0.6351      0.213 0.204 0.000 0.516 0.000 0.280
#&gt; SRR1975454     3  0.6351      0.213 0.204 0.000 0.516 0.000 0.280
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-4-a').click(function(){
  $('#tab-SD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-5'>
<p><a id='tab-SD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     3  0.3619      0.555 0.000 0.000 0.680 0.000 0.316 0.004
#&gt; SRR1975507     3  0.3619      0.555 0.000 0.000 0.680 0.000 0.316 0.004
#&gt; SRR1975506     3  0.3619      0.555 0.000 0.000 0.680 0.000 0.316 0.004
#&gt; SRR1975505     3  0.3619      0.555 0.000 0.000 0.680 0.000 0.316 0.004
#&gt; SRR1975503     4  0.2006      0.897 0.000 0.000 0.004 0.892 0.000 0.104
#&gt; SRR1975504     4  0.2006      0.897 0.000 0.000 0.004 0.892 0.000 0.104
#&gt; SRR1975501     6  0.3927      0.320 0.344 0.000 0.012 0.000 0.000 0.644
#&gt; SRR1975502     6  0.3927      0.320 0.344 0.000 0.012 0.000 0.000 0.644
#&gt; SRR1975499     4  0.0363      0.958 0.000 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1975500     4  0.0363      0.958 0.000 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1975497     1  0.3998      0.424 0.644 0.000 0.016 0.000 0.000 0.340
#&gt; SRR1975498     1  0.3998      0.424 0.644 0.000 0.016 0.000 0.000 0.340
#&gt; SRR1975493     2  0.0363      0.954 0.000 0.988 0.000 0.000 0.000 0.012
#&gt; SRR1975494     2  0.0363      0.954 0.000 0.988 0.000 0.000 0.000 0.012
#&gt; SRR1975495     1  0.3802      0.650 0.748 0.000 0.208 0.000 0.000 0.044
#&gt; SRR1975496     1  0.3802      0.650 0.748 0.000 0.208 0.000 0.000 0.044
#&gt; SRR1975491     6  0.4014      0.490 0.004 0.276 0.024 0.000 0.000 0.696
#&gt; SRR1975492     6  0.4014      0.490 0.004 0.276 0.024 0.000 0.000 0.696
#&gt; SRR1975489     4  0.0146      0.959 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975490     4  0.0146      0.959 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975487     4  0.0146      0.959 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975488     4  0.0146      0.959 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975485     4  0.0000      0.959 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975486     4  0.0000      0.959 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975483     1  0.1918      0.686 0.904 0.000 0.088 0.000 0.000 0.008
#&gt; SRR1975484     1  0.1918      0.686 0.904 0.000 0.088 0.000 0.000 0.008
#&gt; SRR1975481     1  0.2135      0.647 0.872 0.000 0.000 0.000 0.000 0.128
#&gt; SRR1975482     1  0.2135      0.647 0.872 0.000 0.000 0.000 0.000 0.128
#&gt; SRR1975477     5  0.0260      0.884 0.000 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975478     5  0.0260      0.884 0.000 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975479     4  0.2492      0.903 0.000 0.000 0.008 0.888 0.068 0.036
#&gt; SRR1975480     4  0.2492      0.903 0.000 0.000 0.008 0.888 0.068 0.036
#&gt; SRR1975475     4  0.1398      0.944 0.000 0.000 0.008 0.940 0.000 0.052
#&gt; SRR1975476     4  0.1398      0.944 0.000 0.000 0.008 0.940 0.000 0.052
#&gt; SRR1975473     5  0.0260      0.884 0.000 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975474     5  0.0260      0.884 0.000 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975471     1  0.3690      0.613 0.700 0.000 0.288 0.000 0.000 0.012
#&gt; SRR1975472     1  0.3690      0.613 0.700 0.000 0.288 0.000 0.000 0.012
#&gt; SRR1975469     1  0.3997      0.505 0.688 0.000 0.020 0.004 0.000 0.288
#&gt; SRR1975470     1  0.3997      0.505 0.688 0.000 0.020 0.004 0.000 0.288
#&gt; SRR1975467     2  0.2664      0.833 0.000 0.848 0.016 0.000 0.000 0.136
#&gt; SRR1975468     2  0.2664      0.833 0.000 0.848 0.016 0.000 0.000 0.136
#&gt; SRR1975465     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975461     3  0.1720      0.635 0.032 0.000 0.928 0.000 0.040 0.000
#&gt; SRR1975462     3  0.1720      0.635 0.032 0.000 0.928 0.000 0.040 0.000
#&gt; SRR1975459     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.959 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975457     5  0.3248      0.815 0.000 0.000 0.164 0.000 0.804 0.032
#&gt; SRR1975458     5  0.3248      0.815 0.000 0.000 0.164 0.000 0.804 0.032
#&gt; SRR1975455     5  0.2537      0.870 0.000 0.000 0.096 0.000 0.872 0.032
#&gt; SRR1975456     5  0.2537      0.870 0.000 0.000 0.096 0.000 0.872 0.032
#&gt; SRR1975453     3  0.3819      0.252 0.316 0.000 0.672 0.000 0.000 0.012
#&gt; SRR1975454     3  0.3819      0.252 0.316 0.000 0.672 0.000 0.000 0.012
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-5-a').click(function(){
  $('#tab-SD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-skmeans-signature_compare](figure_cola/SD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-skmeans-collect-classes](figure_cola/SD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "pam"]
# you can also extract it by
# res = res_list["SD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-pam-collect-plots](figure_cola/SD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-pam-select-partition-number](figure_cola/SD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.353           0.755       0.854         0.4613 0.494   0.494
#> 3 3 0.467           0.638       0.829         0.3938 0.751   0.538
#> 4 4 0.845           0.869       0.942         0.1804 0.860   0.609
#> 5 5 1.000           0.980       0.991         0.0585 0.917   0.680
#> 6 6 0.915           0.893       0.908         0.0242 0.969   0.848
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 5
```

There is also optional best $k$ = 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-classes'>
<ul>
<li><a href='#tab-SD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-pam-get-classes-1'>
<p><a id='tab-SD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2   0.000      0.917 0.000 1.000
#&gt; SRR1975507     2   0.000      0.917 0.000 1.000
#&gt; SRR1975506     2   0.000      0.917 0.000 1.000
#&gt; SRR1975505     2   0.000      0.917 0.000 1.000
#&gt; SRR1975503     1   0.000      0.696 1.000 0.000
#&gt; SRR1975504     1   0.000      0.696 1.000 0.000
#&gt; SRR1975501     2   0.985      0.269 0.428 0.572
#&gt; SRR1975502     2   0.973      0.312 0.404 0.596
#&gt; SRR1975499     1   0.000      0.696 1.000 0.000
#&gt; SRR1975500     1   0.000      0.696 1.000 0.000
#&gt; SRR1975497     2   0.855      0.554 0.280 0.720
#&gt; SRR1975498     2   0.844      0.571 0.272 0.728
#&gt; SRR1975493     1   0.871      0.724 0.708 0.292
#&gt; SRR1975494     1   0.871      0.724 0.708 0.292
#&gt; SRR1975495     2   0.722      0.629 0.200 0.800
#&gt; SRR1975496     2   0.722      0.629 0.200 0.800
#&gt; SRR1975491     1   0.814      0.737 0.748 0.252
#&gt; SRR1975492     1   0.827      0.735 0.740 0.260
#&gt; SRR1975489     1   0.722      0.635 0.800 0.200
#&gt; SRR1975490     1   0.722      0.635 0.800 0.200
#&gt; SRR1975487     1   0.000      0.696 1.000 0.000
#&gt; SRR1975488     1   0.000      0.696 1.000 0.000
#&gt; SRR1975485     1   0.722      0.635 0.800 0.200
#&gt; SRR1975486     1   0.722      0.635 0.800 0.200
#&gt; SRR1975483     2   0.000      0.917 0.000 1.000
#&gt; SRR1975484     2   0.000      0.917 0.000 1.000
#&gt; SRR1975481     2   0.000      0.917 0.000 1.000
#&gt; SRR1975482     2   0.000      0.917 0.000 1.000
#&gt; SRR1975477     2   0.000      0.917 0.000 1.000
#&gt; SRR1975478     2   0.000      0.917 0.000 1.000
#&gt; SRR1975479     1   1.000      0.490 0.512 0.488
#&gt; SRR1975480     1   1.000      0.490 0.512 0.488
#&gt; SRR1975475     1   0.995      0.544 0.540 0.460
#&gt; SRR1975476     1   0.995      0.544 0.540 0.460
#&gt; SRR1975473     2   0.000      0.917 0.000 1.000
#&gt; SRR1975474     2   0.000      0.917 0.000 1.000
#&gt; SRR1975471     2   0.000      0.917 0.000 1.000
#&gt; SRR1975472     2   0.000      0.917 0.000 1.000
#&gt; SRR1975469     2   0.000      0.917 0.000 1.000
#&gt; SRR1975470     2   0.000      0.917 0.000 1.000
#&gt; SRR1975467     1   0.802      0.738 0.756 0.244
#&gt; SRR1975468     1   0.802      0.738 0.756 0.244
#&gt; SRR1975465     1   0.936      0.683 0.648 0.352
#&gt; SRR1975466     1   0.936      0.683 0.648 0.352
#&gt; SRR1975463     1   0.936      0.683 0.648 0.352
#&gt; SRR1975464     1   0.936      0.683 0.648 0.352
#&gt; SRR1975461     2   0.000      0.917 0.000 1.000
#&gt; SRR1975462     2   0.000      0.917 0.000 1.000
#&gt; SRR1975459     1   0.936      0.683 0.648 0.352
#&gt; SRR1975460     1   0.936      0.683 0.648 0.352
#&gt; SRR1975457     2   0.000      0.917 0.000 1.000
#&gt; SRR1975458     2   0.000      0.917 0.000 1.000
#&gt; SRR1975455     2   0.000      0.917 0.000 1.000
#&gt; SRR1975456     2   0.000      0.917 0.000 1.000
#&gt; SRR1975453     2   0.000      0.917 0.000 1.000
#&gt; SRR1975454     2   0.000      0.917 0.000 1.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-1-a').click(function(){
  $('#tab-SD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-2'>
<p><a id='tab-SD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.6192     0.4330 0.000 0.420 0.580
#&gt; SRR1975507     3  0.6079     0.4920 0.000 0.388 0.612
#&gt; SRR1975506     3  0.6062     0.4975 0.000 0.384 0.616
#&gt; SRR1975505     3  0.6154     0.4575 0.000 0.408 0.592
#&gt; SRR1975503     1  0.0000     0.8199 1.000 0.000 0.000
#&gt; SRR1975504     1  0.0000     0.8199 1.000 0.000 0.000
#&gt; SRR1975501     3  0.4750     0.6188 0.000 0.216 0.784
#&gt; SRR1975502     3  0.4750     0.6188 0.000 0.216 0.784
#&gt; SRR1975499     1  0.0000     0.8199 1.000 0.000 0.000
#&gt; SRR1975500     1  0.0000     0.8199 1.000 0.000 0.000
#&gt; SRR1975497     3  0.0747     0.7998 0.000 0.016 0.984
#&gt; SRR1975498     3  0.0892     0.7975 0.000 0.020 0.980
#&gt; SRR1975493     2  0.4346     0.7154 0.184 0.816 0.000
#&gt; SRR1975494     2  0.4346     0.7154 0.184 0.816 0.000
#&gt; SRR1975495     3  0.4452     0.6429 0.000 0.192 0.808
#&gt; SRR1975496     3  0.4452     0.6429 0.000 0.192 0.808
#&gt; SRR1975491     2  0.7431     0.5959 0.188 0.696 0.116
#&gt; SRR1975492     2  0.7558     0.5854 0.188 0.688 0.124
#&gt; SRR1975489     1  0.0000     0.8199 1.000 0.000 0.000
#&gt; SRR1975490     1  0.0000     0.8199 1.000 0.000 0.000
#&gt; SRR1975487     1  0.0000     0.8199 1.000 0.000 0.000
#&gt; SRR1975488     1  0.0000     0.8199 1.000 0.000 0.000
#&gt; SRR1975485     1  0.0000     0.8199 1.000 0.000 0.000
#&gt; SRR1975486     1  0.0000     0.8199 1.000 0.000 0.000
#&gt; SRR1975483     3  0.0000     0.8073 0.000 0.000 1.000
#&gt; SRR1975484     3  0.0000     0.8073 0.000 0.000 1.000
#&gt; SRR1975481     3  0.0000     0.8073 0.000 0.000 1.000
#&gt; SRR1975482     3  0.0000     0.8073 0.000 0.000 1.000
#&gt; SRR1975477     2  0.4452     0.5484 0.000 0.808 0.192
#&gt; SRR1975478     2  0.4452     0.5484 0.000 0.808 0.192
#&gt; SRR1975479     1  0.8722     0.3490 0.592 0.216 0.192
#&gt; SRR1975480     1  0.8722     0.3490 0.592 0.216 0.192
#&gt; SRR1975475     1  0.9502    -0.0927 0.436 0.376 0.188
#&gt; SRR1975476     1  0.9161     0.2092 0.532 0.280 0.188
#&gt; SRR1975473     2  0.4504     0.5483 0.000 0.804 0.196
#&gt; SRR1975474     2  0.4504     0.5483 0.000 0.804 0.196
#&gt; SRR1975471     3  0.0000     0.8073 0.000 0.000 1.000
#&gt; SRR1975472     3  0.0000     0.8073 0.000 0.000 1.000
#&gt; SRR1975469     3  0.0000     0.8073 0.000 0.000 1.000
#&gt; SRR1975470     3  0.0000     0.8073 0.000 0.000 1.000
#&gt; SRR1975467     2  0.4399     0.7118 0.188 0.812 0.000
#&gt; SRR1975468     2  0.4399     0.7118 0.188 0.812 0.000
#&gt; SRR1975465     2  0.4062     0.7266 0.164 0.836 0.000
#&gt; SRR1975466     2  0.4062     0.7266 0.164 0.836 0.000
#&gt; SRR1975463     2  0.4062     0.7266 0.164 0.836 0.000
#&gt; SRR1975464     2  0.4062     0.7266 0.164 0.836 0.000
#&gt; SRR1975461     3  0.4062     0.7307 0.000 0.164 0.836
#&gt; SRR1975462     3  0.4062     0.7307 0.000 0.164 0.836
#&gt; SRR1975459     2  0.4062     0.7266 0.164 0.836 0.000
#&gt; SRR1975460     2  0.4062     0.7266 0.164 0.836 0.000
#&gt; SRR1975457     2  0.6295    -0.1909 0.000 0.528 0.472
#&gt; SRR1975458     2  0.6295    -0.1909 0.000 0.528 0.472
#&gt; SRR1975455     3  0.6126     0.4738 0.000 0.400 0.600
#&gt; SRR1975456     3  0.6126     0.4738 0.000 0.400 0.600
#&gt; SRR1975453     3  0.0000     0.8073 0.000 0.000 1.000
#&gt; SRR1975454     3  0.0000     0.8073 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-2-a').click(function(){
  $('#tab-SD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-3'>
<p><a id='tab-SD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3   0.000      0.914 0.000 0.000 1.000 0.000
#&gt; SRR1975507     3   0.000      0.914 0.000 0.000 1.000 0.000
#&gt; SRR1975506     3   0.000      0.914 0.000 0.000 1.000 0.000
#&gt; SRR1975505     3   0.000      0.914 0.000 0.000 1.000 0.000
#&gt; SRR1975503     4   0.000      0.907 0.000 0.000 0.000 1.000
#&gt; SRR1975504     4   0.000      0.907 0.000 0.000 0.000 1.000
#&gt; SRR1975501     1   0.391      0.720 0.768 0.232 0.000 0.000
#&gt; SRR1975502     1   0.391      0.720 0.768 0.232 0.000 0.000
#&gt; SRR1975499     4   0.000      0.907 0.000 0.000 0.000 1.000
#&gt; SRR1975500     4   0.000      0.907 0.000 0.000 0.000 1.000
#&gt; SRR1975497     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975498     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975493     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975494     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975495     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975496     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975491     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975492     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975489     4   0.000      0.907 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4   0.000      0.907 0.000 0.000 0.000 1.000
#&gt; SRR1975487     4   0.000      0.907 0.000 0.000 0.000 1.000
#&gt; SRR1975488     4   0.000      0.907 0.000 0.000 0.000 1.000
#&gt; SRR1975485     4   0.000      0.907 0.000 0.000 0.000 1.000
#&gt; SRR1975486     4   0.000      0.907 0.000 0.000 0.000 1.000
#&gt; SRR1975483     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975484     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975481     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975482     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975477     3   0.384      0.687 0.000 0.224 0.776 0.000
#&gt; SRR1975478     3   0.387      0.681 0.000 0.228 0.772 0.000
#&gt; SRR1975479     4   0.327      0.785 0.000 0.000 0.168 0.832
#&gt; SRR1975480     4   0.327      0.785 0.000 0.000 0.168 0.832
#&gt; SRR1975475     4   0.751      0.285 0.000 0.336 0.196 0.468
#&gt; SRR1975476     4   0.646      0.608 0.000 0.160 0.196 0.644
#&gt; SRR1975473     2   0.480      0.370 0.000 0.616 0.384 0.000
#&gt; SRR1975474     2   0.480      0.370 0.000 0.616 0.384 0.000
#&gt; SRR1975471     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975472     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975469     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975470     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975467     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975468     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975465     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975466     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975463     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975464     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975461     3   0.327      0.777 0.168 0.000 0.832 0.000
#&gt; SRR1975462     3   0.327      0.777 0.168 0.000 0.832 0.000
#&gt; SRR1975459     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975460     2   0.000      0.934 0.000 1.000 0.000 0.000
#&gt; SRR1975457     3   0.000      0.914 0.000 0.000 1.000 0.000
#&gt; SRR1975458     3   0.000      0.914 0.000 0.000 1.000 0.000
#&gt; SRR1975455     3   0.000      0.914 0.000 0.000 1.000 0.000
#&gt; SRR1975456     3   0.000      0.914 0.000 0.000 1.000 0.000
#&gt; SRR1975453     1   0.000      0.966 1.000 0.000 0.000 0.000
#&gt; SRR1975454     1   0.000      0.966 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-3-a').click(function(){
  $('#tab-SD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-4'>
<p><a id='tab-SD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4    p5
#&gt; SRR1975508     3   0.000      0.995 0.000 0.000 1.000  0 0.000
#&gt; SRR1975507     3   0.000      0.995 0.000 0.000 1.000  0 0.000
#&gt; SRR1975506     3   0.000      0.995 0.000 0.000 1.000  0 0.000
#&gt; SRR1975505     3   0.000      0.995 0.000 0.000 1.000  0 0.000
#&gt; SRR1975503     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975504     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975501     1   0.337      0.718 0.768 0.232 0.000  0 0.000
#&gt; SRR1975502     1   0.337      0.718 0.768 0.232 0.000  0 0.000
#&gt; SRR1975499     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975500     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975497     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975498     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975493     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975494     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975495     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975496     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975491     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975492     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975489     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975490     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975487     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975488     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975485     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975486     4   0.000      1.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975483     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975484     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975481     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975482     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975477     5   0.000      1.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975478     5   0.000      1.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975479     5   0.000      1.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975480     5   0.000      1.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975475     5   0.000      1.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975476     5   0.000      1.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975473     5   0.000      1.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975474     5   0.000      1.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975471     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975472     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975469     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975470     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975467     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975468     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975465     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975466     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975463     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975464     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975461     3   0.000      0.995 0.000 0.000 1.000  0 0.000
#&gt; SRR1975462     3   0.000      0.995 0.000 0.000 1.000  0 0.000
#&gt; SRR1975459     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975460     2   0.000      1.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1975457     3   0.051      0.986 0.000 0.000 0.984  0 0.016
#&gt; SRR1975458     3   0.051      0.986 0.000 0.000 0.984  0 0.016
#&gt; SRR1975455     5   0.000      1.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975456     5   0.000      1.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975453     1   0.000      0.966 1.000 0.000 0.000  0 0.000
#&gt; SRR1975454     1   0.000      0.966 1.000 0.000 0.000  0 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-4-a').click(function(){
  $('#tab-SD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-5'>
<p><a id='tab-SD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975503     4  0.3351      0.794 0.000 0.000 0.000 0.712 0.000 0.288
#&gt; SRR1975504     4  0.3351      0.794 0.000 0.000 0.000 0.712 0.000 0.288
#&gt; SRR1975501     1  0.4918      0.597 0.644 0.232 0.000 0.000 0.000 0.124
#&gt; SRR1975502     1  0.4918      0.597 0.644 0.232 0.000 0.000 0.000 0.124
#&gt; SRR1975499     4  0.3351      0.794 0.000 0.000 0.000 0.712 0.000 0.288
#&gt; SRR1975500     4  0.3351      0.794 0.000 0.000 0.000 0.712 0.000 0.288
#&gt; SRR1975497     1  0.2378      0.839 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1975498     1  0.2378      0.839 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1975493     2  0.0000      0.992 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975494     2  0.0000      0.992 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975495     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975491     2  0.1007      0.959 0.000 0.956 0.000 0.000 0.000 0.044
#&gt; SRR1975492     2  0.1007      0.959 0.000 0.956 0.000 0.000 0.000 0.044
#&gt; SRR1975489     4  0.0260      0.799 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1975490     4  0.0260      0.799 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1975487     4  0.3151      0.801 0.000 0.000 0.000 0.748 0.000 0.252
#&gt; SRR1975488     4  0.0146      0.803 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975485     4  0.0000      0.803 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975486     4  0.0000      0.803 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975483     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975477     5  0.0000      0.919 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975478     5  0.0000      0.919 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975479     6  0.5522      0.772 0.000 0.000 0.000 0.256 0.188 0.556
#&gt; SRR1975480     6  0.5522      0.772 0.000 0.000 0.000 0.256 0.188 0.556
#&gt; SRR1975475     6  0.2664      0.773 0.000 0.000 0.000 0.000 0.184 0.816
#&gt; SRR1975476     6  0.2664      0.773 0.000 0.000 0.000 0.000 0.184 0.816
#&gt; SRR1975473     5  0.0000      0.919 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975474     5  0.0000      0.919 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975471     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975469     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975470     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975467     2  0.0000      0.992 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975468     2  0.0000      0.992 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975465     2  0.0000      0.992 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.992 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.992 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.992 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975461     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975462     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975459     2  0.0000      0.992 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.992 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975457     5  0.2664      0.763 0.000 0.000 0.184 0.000 0.816 0.000
#&gt; SRR1975458     5  0.2664      0.763 0.000 0.000 0.184 0.000 0.816 0.000
#&gt; SRR1975455     5  0.0000      0.919 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975456     5  0.0000      0.919 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975453     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975454     1  0.0000      0.932 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-5-a').click(function(){
  $('#tab-SD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-SD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-pam-signature_compare](figure_cola/SD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-SD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-pam-collect-classes](figure_cola/SD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:mclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "mclust"]
# you can also extract it by
# res = res_list["SD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-mclust-collect-plots](figure_cola/SD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-mclust-select-partition-number](figure_cola/SD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.532           0.944       0.955         0.3634 0.657   0.657
#> 3 3 0.572           0.633       0.825         0.6753 0.727   0.585
#> 4 4 0.997           0.975       0.985         0.2499 0.855   0.622
#> 5 5 0.961           0.895       0.956         0.0447 0.945   0.779
#> 6 6 0.919           0.883       0.931         0.0463 0.961   0.805
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 4 5
```

There is also optional best $k$ = 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-classes'>
<ul>
<li><a href='#tab-SD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-mclust-get-classes-1'>
<p><a id='tab-SD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2   0.000      1.000 0.000 1.000
#&gt; SRR1975507     2   0.000      1.000 0.000 1.000
#&gt; SRR1975506     2   0.000      1.000 0.000 1.000
#&gt; SRR1975505     2   0.000      1.000 0.000 1.000
#&gt; SRR1975503     1   0.000      0.936 1.000 0.000
#&gt; SRR1975504     1   0.000      0.936 1.000 0.000
#&gt; SRR1975501     1   0.552      0.918 0.872 0.128
#&gt; SRR1975502     1   0.552      0.918 0.872 0.128
#&gt; SRR1975499     1   0.000      0.936 1.000 0.000
#&gt; SRR1975500     1   0.000      0.936 1.000 0.000
#&gt; SRR1975497     1   0.552      0.918 0.872 0.128
#&gt; SRR1975498     1   0.552      0.918 0.872 0.128
#&gt; SRR1975493     1   0.000      0.936 1.000 0.000
#&gt; SRR1975494     1   0.000      0.936 1.000 0.000
#&gt; SRR1975495     1   0.552      0.918 0.872 0.128
#&gt; SRR1975496     1   0.552      0.918 0.872 0.128
#&gt; SRR1975491     1   0.506      0.921 0.888 0.112
#&gt; SRR1975492     1   0.506      0.921 0.888 0.112
#&gt; SRR1975489     1   0.000      0.936 1.000 0.000
#&gt; SRR1975490     1   0.000      0.936 1.000 0.000
#&gt; SRR1975487     1   0.000      0.936 1.000 0.000
#&gt; SRR1975488     1   0.000      0.936 1.000 0.000
#&gt; SRR1975485     1   0.000      0.936 1.000 0.000
#&gt; SRR1975486     1   0.000      0.936 1.000 0.000
#&gt; SRR1975483     1   0.552      0.918 0.872 0.128
#&gt; SRR1975484     1   0.552      0.918 0.872 0.128
#&gt; SRR1975481     1   0.552      0.918 0.872 0.128
#&gt; SRR1975482     1   0.552      0.918 0.872 0.128
#&gt; SRR1975477     2   0.000      1.000 0.000 1.000
#&gt; SRR1975478     2   0.000      1.000 0.000 1.000
#&gt; SRR1975479     1   0.000      0.936 1.000 0.000
#&gt; SRR1975480     1   0.000      0.936 1.000 0.000
#&gt; SRR1975475     1   0.000      0.936 1.000 0.000
#&gt; SRR1975476     1   0.000      0.936 1.000 0.000
#&gt; SRR1975473     2   0.000      1.000 0.000 1.000
#&gt; SRR1975474     2   0.000      1.000 0.000 1.000
#&gt; SRR1975471     1   0.552      0.918 0.872 0.128
#&gt; SRR1975472     1   0.552      0.918 0.872 0.128
#&gt; SRR1975469     1   0.552      0.918 0.872 0.128
#&gt; SRR1975470     1   0.552      0.918 0.872 0.128
#&gt; SRR1975467     1   0.000      0.936 1.000 0.000
#&gt; SRR1975468     1   0.000      0.936 1.000 0.000
#&gt; SRR1975465     1   0.000      0.936 1.000 0.000
#&gt; SRR1975466     1   0.000      0.936 1.000 0.000
#&gt; SRR1975463     1   0.000      0.936 1.000 0.000
#&gt; SRR1975464     1   0.000      0.936 1.000 0.000
#&gt; SRR1975461     1   0.552      0.918 0.872 0.128
#&gt; SRR1975462     1   0.552      0.918 0.872 0.128
#&gt; SRR1975459     1   0.000      0.936 1.000 0.000
#&gt; SRR1975460     1   0.000      0.936 1.000 0.000
#&gt; SRR1975457     2   0.000      1.000 0.000 1.000
#&gt; SRR1975458     2   0.000      1.000 0.000 1.000
#&gt; SRR1975455     2   0.000      1.000 0.000 1.000
#&gt; SRR1975456     2   0.000      1.000 0.000 1.000
#&gt; SRR1975453     1   0.552      0.918 0.872 0.128
#&gt; SRR1975454     1   0.552      0.918 0.872 0.128
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-1-a').click(function(){
  $('#tab-SD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-2'>
<p><a id='tab-SD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975507     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975506     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975505     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975503     1  0.9566     0.3276 0.424 0.380 0.196
#&gt; SRR1975504     1  0.9566     0.3276 0.424 0.380 0.196
#&gt; SRR1975501     2  0.6225     0.0938 0.432 0.568 0.000
#&gt; SRR1975502     2  0.6225     0.0938 0.432 0.568 0.000
#&gt; SRR1975499     1  0.9633     0.3455 0.424 0.368 0.208
#&gt; SRR1975500     1  0.9633     0.3455 0.424 0.368 0.208
#&gt; SRR1975497     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975498     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975493     2  0.0237     0.8025 0.000 0.996 0.004
#&gt; SRR1975494     2  0.0237     0.8025 0.000 0.996 0.004
#&gt; SRR1975495     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975496     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975491     2  0.6215     0.1003 0.428 0.572 0.000
#&gt; SRR1975492     2  0.6215     0.1003 0.428 0.572 0.000
#&gt; SRR1975489     1  0.9647     0.3531 0.428 0.360 0.212
#&gt; SRR1975490     1  0.9647     0.3531 0.428 0.360 0.212
#&gt; SRR1975487     1  0.9653     0.3493 0.424 0.364 0.212
#&gt; SRR1975488     1  0.9653     0.3493 0.424 0.364 0.212
#&gt; SRR1975485     1  0.9621     0.3539 0.432 0.360 0.208
#&gt; SRR1975486     1  0.9621     0.3539 0.432 0.360 0.208
#&gt; SRR1975483     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975484     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975481     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975482     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975477     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975478     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975479     1  0.9647     0.3531 0.428 0.360 0.212
#&gt; SRR1975480     1  0.9647     0.3531 0.428 0.360 0.212
#&gt; SRR1975475     1  0.9672     0.3469 0.424 0.360 0.216
#&gt; SRR1975476     1  0.9672     0.3469 0.424 0.360 0.216
#&gt; SRR1975473     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975474     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975471     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975472     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975469     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975470     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975467     2  0.0237     0.8025 0.000 0.996 0.004
#&gt; SRR1975468     2  0.0237     0.8025 0.000 0.996 0.004
#&gt; SRR1975465     2  0.0237     0.8025 0.000 0.996 0.004
#&gt; SRR1975466     2  0.0237     0.8025 0.000 0.996 0.004
#&gt; SRR1975463     2  0.0237     0.8025 0.000 0.996 0.004
#&gt; SRR1975464     2  0.0237     0.8025 0.000 0.996 0.004
#&gt; SRR1975461     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975462     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975459     2  0.0237     0.8025 0.000 0.996 0.004
#&gt; SRR1975460     2  0.0237     0.8025 0.000 0.996 0.004
#&gt; SRR1975457     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975458     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975455     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975456     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975453     1  0.0000     0.6366 1.000 0.000 0.000
#&gt; SRR1975454     1  0.0000     0.6366 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-2-a').click(function(){
  $('#tab-SD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-3'>
<p><a id='tab-SD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975503     4  0.1584      0.959 0.000 0.036 0.012 0.952
#&gt; SRR1975504     4  0.1584      0.959 0.000 0.036 0.012 0.952
#&gt; SRR1975501     2  0.0672      0.974 0.008 0.984 0.000 0.008
#&gt; SRR1975502     2  0.0672      0.974 0.008 0.984 0.000 0.008
#&gt; SRR1975499     4  0.0188      0.990 0.000 0.004 0.000 0.996
#&gt; SRR1975500     4  0.0188      0.990 0.000 0.004 0.000 0.996
#&gt; SRR1975497     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975493     2  0.1474      0.951 0.000 0.948 0.052 0.000
#&gt; SRR1975494     2  0.1474      0.951 0.000 0.948 0.052 0.000
#&gt; SRR1975495     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975491     2  0.0672      0.974 0.008 0.984 0.000 0.008
#&gt; SRR1975492     2  0.0672      0.974 0.008 0.984 0.000 0.008
#&gt; SRR1975489     4  0.0000      0.993 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4  0.0000      0.993 0.000 0.000 0.000 1.000
#&gt; SRR1975487     4  0.0000      0.993 0.000 0.000 0.000 1.000
#&gt; SRR1975488     4  0.0000      0.993 0.000 0.000 0.000 1.000
#&gt; SRR1975485     4  0.0000      0.993 0.000 0.000 0.000 1.000
#&gt; SRR1975486     4  0.0000      0.993 0.000 0.000 0.000 1.000
#&gt; SRR1975483     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975477     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975478     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975479     4  0.0000      0.993 0.000 0.000 0.000 1.000
#&gt; SRR1975480     4  0.0000      0.993 0.000 0.000 0.000 1.000
#&gt; SRR1975475     4  0.0000      0.993 0.000 0.000 0.000 1.000
#&gt; SRR1975476     4  0.0000      0.993 0.000 0.000 0.000 1.000
#&gt; SRR1975473     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975474     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975471     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975469     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975470     1  0.0000      0.971 1.000 0.000 0.000 0.000
#&gt; SRR1975467     2  0.2124      0.935 0.000 0.924 0.068 0.008
#&gt; SRR1975468     2  0.2124      0.935 0.000 0.924 0.068 0.008
#&gt; SRR1975465     2  0.0000      0.976 0.000 1.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.976 0.000 1.000 0.000 0.000
#&gt; SRR1975463     2  0.0188      0.976 0.000 0.996 0.004 0.000
#&gt; SRR1975464     2  0.0188      0.976 0.000 0.996 0.004 0.000
#&gt; SRR1975461     1  0.2814      0.875 0.868 0.000 0.132 0.000
#&gt; SRR1975462     1  0.2814      0.875 0.868 0.000 0.132 0.000
#&gt; SRR1975459     2  0.0000      0.976 0.000 1.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.976 0.000 1.000 0.000 0.000
#&gt; SRR1975457     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975458     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975455     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975456     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975453     1  0.2081      0.919 0.916 0.000 0.084 0.000
#&gt; SRR1975454     1  0.2081      0.919 0.916 0.000 0.084 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-3-a').click(function(){
  $('#tab-SD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-4'>
<p><a id='tab-SD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975503     5  0.4283      0.171 0.000 0.000  0 0.456 0.544
#&gt; SRR1975504     5  0.4283      0.171 0.000 0.000  0 0.456 0.544
#&gt; SRR1975501     5  0.0162      0.707 0.004 0.000  0 0.000 0.996
#&gt; SRR1975502     5  0.0162      0.707 0.004 0.000  0 0.000 0.996
#&gt; SRR1975499     4  0.3684      0.556 0.000 0.000  0 0.720 0.280
#&gt; SRR1975500     4  0.3684      0.556 0.000 0.000  0 0.720 0.280
#&gt; SRR1975497     1  0.0162      0.996 0.996 0.000  0 0.000 0.004
#&gt; SRR1975498     1  0.0162      0.996 0.996 0.000  0 0.000 0.004
#&gt; SRR1975493     2  0.0000      1.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1975494     2  0.0000      1.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1975495     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975491     5  0.0000      0.708 0.000 0.000  0 0.000 1.000
#&gt; SRR1975492     5  0.0000      0.708 0.000 0.000  0 0.000 1.000
#&gt; SRR1975489     4  0.0000      0.930 0.000 0.000  0 1.000 0.000
#&gt; SRR1975490     4  0.0000      0.930 0.000 0.000  0 1.000 0.000
#&gt; SRR1975487     4  0.0000      0.930 0.000 0.000  0 1.000 0.000
#&gt; SRR1975488     4  0.0000      0.930 0.000 0.000  0 1.000 0.000
#&gt; SRR1975485     4  0.0000      0.930 0.000 0.000  0 1.000 0.000
#&gt; SRR1975486     4  0.0000      0.930 0.000 0.000  0 1.000 0.000
#&gt; SRR1975483     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975477     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975478     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975479     4  0.0404      0.929 0.000 0.000  0 0.988 0.012
#&gt; SRR1975480     4  0.0404      0.929 0.000 0.000  0 0.988 0.012
#&gt; SRR1975475     4  0.0404      0.929 0.000 0.000  0 0.988 0.012
#&gt; SRR1975476     4  0.0404      0.929 0.000 0.000  0 0.988 0.012
#&gt; SRR1975473     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975474     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975471     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975469     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975470     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975467     5  0.4283      0.270 0.000 0.456  0 0.000 0.544
#&gt; SRR1975468     5  0.4283      0.270 0.000 0.456  0 0.000 0.544
#&gt; SRR1975465     2  0.0000      1.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1975466     2  0.0000      1.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1975463     2  0.0000      1.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1975464     2  0.0000      1.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1975461     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975462     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975459     2  0.0000      1.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1975460     2  0.0000      1.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1975457     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975458     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975455     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975456     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975453     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
#&gt; SRR1975454     1  0.0000      0.999 1.000 0.000  0 0.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-4-a').click(function(){
  $('#tab-SD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-5'>
<p><a id='tab-SD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5    p6
#&gt; SRR1975508     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975507     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975506     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975505     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975503     6  0.5495      0.146 0.000 0.000 0.128 0.404  0 0.468
#&gt; SRR1975504     6  0.5495      0.146 0.000 0.000 0.128 0.404  0 0.468
#&gt; SRR1975501     6  0.0146      0.668 0.004 0.000 0.000 0.000  0 0.996
#&gt; SRR1975502     6  0.0146      0.668 0.004 0.000 0.000 0.000  0 0.996
#&gt; SRR1975499     4  0.4847      0.526 0.000 0.000 0.124 0.656  0 0.220
#&gt; SRR1975500     4  0.4847      0.526 0.000 0.000 0.124 0.656  0 0.220
#&gt; SRR1975497     1  0.0000      0.995 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975498     1  0.0000      0.995 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975493     2  0.0000      1.000 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975494     2  0.0000      1.000 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975495     1  0.0547      0.979 0.980 0.000 0.020 0.000  0 0.000
#&gt; SRR1975496     1  0.0547      0.979 0.980 0.000 0.020 0.000  0 0.000
#&gt; SRR1975491     6  0.0000      0.669 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975492     6  0.0000      0.669 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975489     4  0.0000      0.905 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975490     4  0.0000      0.905 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975487     4  0.0000      0.905 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975488     4  0.0000      0.905 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975485     4  0.0000      0.905 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975486     4  0.0000      0.905 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975483     1  0.0000      0.995 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975484     1  0.0000      0.995 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975481     1  0.0000      0.995 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975482     1  0.0000      0.995 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975477     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975478     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975479     4  0.1267      0.898 0.000 0.000 0.060 0.940  0 0.000
#&gt; SRR1975480     4  0.1267      0.898 0.000 0.000 0.060 0.940  0 0.000
#&gt; SRR1975475     4  0.1267      0.898 0.000 0.000 0.060 0.940  0 0.000
#&gt; SRR1975476     4  0.1267      0.898 0.000 0.000 0.060 0.940  0 0.000
#&gt; SRR1975473     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975474     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975471     3  0.2135      1.000 0.128 0.000 0.872 0.000  0 0.000
#&gt; SRR1975472     3  0.2135      1.000 0.128 0.000 0.872 0.000  0 0.000
#&gt; SRR1975469     1  0.0000      0.995 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975470     1  0.0000      0.995 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975467     6  0.5189      0.245 0.000 0.444 0.088 0.000  0 0.468
#&gt; SRR1975468     6  0.5189      0.245 0.000 0.444 0.088 0.000  0 0.468
#&gt; SRR1975465     2  0.0000      1.000 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975466     2  0.0000      1.000 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975463     2  0.0000      1.000 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975464     2  0.0000      1.000 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975461     3  0.2135      1.000 0.128 0.000 0.872 0.000  0 0.000
#&gt; SRR1975462     3  0.2135      1.000 0.128 0.000 0.872 0.000  0 0.000
#&gt; SRR1975459     2  0.0000      1.000 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975460     2  0.0000      1.000 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975457     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975458     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975455     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975456     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975453     3  0.2135      1.000 0.128 0.000 0.872 0.000  0 0.000
#&gt; SRR1975454     3  0.2135      1.000 0.128 0.000 0.872 0.000  0 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-5-a').click(function(){
  $('#tab-SD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-mclust-signature_compare](figure_cola/SD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-mclust-collect-classes](figure_cola/SD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "NMF"]
# you can also extract it by
# res = res_list["SD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-NMF-collect-plots](figure_cola/SD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-NMF-select-partition-number](figure_cola/SD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.981       0.991         0.5090 0.491   0.491
#> 3 3 0.739           0.685       0.876         0.3099 0.718   0.485
#> 4 4 0.824           0.926       0.930         0.1281 0.853   0.587
#> 5 5 0.846           0.792       0.877         0.0555 0.964   0.851
#> 6 6 0.813           0.760       0.847         0.0382 0.958   0.805
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-classes'>
<ul>
<li><a href='#tab-SD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-NMF-get-classes-1'>
<p><a id='tab-SD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2   0.000      0.983 0.000 1.000
#&gt; SRR1975507     2   0.000      0.983 0.000 1.000
#&gt; SRR1975506     2   0.000      0.983 0.000 1.000
#&gt; SRR1975505     2   0.000      0.983 0.000 1.000
#&gt; SRR1975503     1   0.000      0.998 1.000 0.000
#&gt; SRR1975504     1   0.000      0.998 1.000 0.000
#&gt; SRR1975501     2   0.000      0.983 0.000 1.000
#&gt; SRR1975502     2   0.000      0.983 0.000 1.000
#&gt; SRR1975499     1   0.000      0.998 1.000 0.000
#&gt; SRR1975500     1   0.000      0.998 1.000 0.000
#&gt; SRR1975497     2   0.000      0.983 0.000 1.000
#&gt; SRR1975498     2   0.000      0.983 0.000 1.000
#&gt; SRR1975493     1   0.000      0.998 1.000 0.000
#&gt; SRR1975494     1   0.000      0.998 1.000 0.000
#&gt; SRR1975495     2   0.000      0.983 0.000 1.000
#&gt; SRR1975496     2   0.000      0.983 0.000 1.000
#&gt; SRR1975491     1   0.000      0.998 1.000 0.000
#&gt; SRR1975492     1   0.000      0.998 1.000 0.000
#&gt; SRR1975489     1   0.000      0.998 1.000 0.000
#&gt; SRR1975490     1   0.000      0.998 1.000 0.000
#&gt; SRR1975487     1   0.000      0.998 1.000 0.000
#&gt; SRR1975488     1   0.000      0.998 1.000 0.000
#&gt; SRR1975485     1   0.000      0.998 1.000 0.000
#&gt; SRR1975486     1   0.000      0.998 1.000 0.000
#&gt; SRR1975483     2   0.000      0.983 0.000 1.000
#&gt; SRR1975484     2   0.000      0.983 0.000 1.000
#&gt; SRR1975481     2   0.000      0.983 0.000 1.000
#&gt; SRR1975482     2   0.000      0.983 0.000 1.000
#&gt; SRR1975477     2   0.760      0.727 0.220 0.780
#&gt; SRR1975478     2   0.760      0.727 0.220 0.780
#&gt; SRR1975479     1   0.000      0.998 1.000 0.000
#&gt; SRR1975480     1   0.000      0.998 1.000 0.000
#&gt; SRR1975475     1   0.000      0.998 1.000 0.000
#&gt; SRR1975476     1   0.000      0.998 1.000 0.000
#&gt; SRR1975473     1   0.163      0.976 0.976 0.024
#&gt; SRR1975474     1   0.163      0.976 0.976 0.024
#&gt; SRR1975471     2   0.000      0.983 0.000 1.000
#&gt; SRR1975472     2   0.000      0.983 0.000 1.000
#&gt; SRR1975469     2   0.000      0.983 0.000 1.000
#&gt; SRR1975470     2   0.000      0.983 0.000 1.000
#&gt; SRR1975467     1   0.000      0.998 1.000 0.000
#&gt; SRR1975468     1   0.000      0.998 1.000 0.000
#&gt; SRR1975465     1   0.000      0.998 1.000 0.000
#&gt; SRR1975466     1   0.000      0.998 1.000 0.000
#&gt; SRR1975463     1   0.000      0.998 1.000 0.000
#&gt; SRR1975464     1   0.000      0.998 1.000 0.000
#&gt; SRR1975461     2   0.000      0.983 0.000 1.000
#&gt; SRR1975462     2   0.000      0.983 0.000 1.000
#&gt; SRR1975459     1   0.000      0.998 1.000 0.000
#&gt; SRR1975460     1   0.000      0.998 1.000 0.000
#&gt; SRR1975457     2   0.000      0.983 0.000 1.000
#&gt; SRR1975458     2   0.000      0.983 0.000 1.000
#&gt; SRR1975455     2   0.000      0.983 0.000 1.000
#&gt; SRR1975456     2   0.000      0.983 0.000 1.000
#&gt; SRR1975453     2   0.000      0.983 0.000 1.000
#&gt; SRR1975454     2   0.000      0.983 0.000 1.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-1-a').click(function(){
  $('#tab-SD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-2'>
<p><a id='tab-SD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.6291      0.369 0.468 0.000 0.532
#&gt; SRR1975507     3  0.6295      0.360 0.472 0.000 0.528
#&gt; SRR1975506     3  0.6295      0.360 0.472 0.000 0.528
#&gt; SRR1975505     3  0.6280      0.383 0.460 0.000 0.540
#&gt; SRR1975503     2  0.1643      0.909 0.000 0.956 0.044
#&gt; SRR1975504     2  0.1643      0.909 0.000 0.956 0.044
#&gt; SRR1975501     1  0.6286      0.084 0.536 0.464 0.000
#&gt; SRR1975502     1  0.6286      0.084 0.536 0.464 0.000
#&gt; SRR1975499     2  0.5058      0.723 0.000 0.756 0.244
#&gt; SRR1975500     2  0.4974      0.733 0.000 0.764 0.236
#&gt; SRR1975497     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975493     2  0.0000      0.932 0.000 1.000 0.000
#&gt; SRR1975494     2  0.0000      0.932 0.000 1.000 0.000
#&gt; SRR1975495     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975491     2  0.0237      0.930 0.004 0.996 0.000
#&gt; SRR1975492     2  0.0237      0.930 0.004 0.996 0.000
#&gt; SRR1975489     3  0.0237      0.732 0.000 0.004 0.996
#&gt; SRR1975490     3  0.0237      0.732 0.000 0.004 0.996
#&gt; SRR1975487     2  0.6307      0.302 0.000 0.512 0.488
#&gt; SRR1975488     3  0.6235     -0.179 0.000 0.436 0.564
#&gt; SRR1975485     3  0.0424      0.730 0.000 0.008 0.992
#&gt; SRR1975486     3  0.0424      0.730 0.000 0.008 0.992
#&gt; SRR1975483     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975477     3  0.5760      0.545 0.328 0.000 0.672
#&gt; SRR1975478     3  0.5760      0.545 0.328 0.000 0.672
#&gt; SRR1975479     3  0.0237      0.732 0.000 0.004 0.996
#&gt; SRR1975480     3  0.0237      0.732 0.000 0.004 0.996
#&gt; SRR1975475     3  0.0237      0.732 0.000 0.004 0.996
#&gt; SRR1975476     3  0.0237      0.732 0.000 0.004 0.996
#&gt; SRR1975473     3  0.0237      0.731 0.004 0.000 0.996
#&gt; SRR1975474     3  0.0237      0.731 0.004 0.000 0.996
#&gt; SRR1975471     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975469     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975470     1  0.0000      0.855 1.000 0.000 0.000
#&gt; SRR1975467     2  0.0000      0.932 0.000 1.000 0.000
#&gt; SRR1975468     2  0.0000      0.932 0.000 1.000 0.000
#&gt; SRR1975465     2  0.0000      0.932 0.000 1.000 0.000
#&gt; SRR1975466     2  0.0000      0.932 0.000 1.000 0.000
#&gt; SRR1975463     2  0.0000      0.932 0.000 1.000 0.000
#&gt; SRR1975464     2  0.0000      0.932 0.000 1.000 0.000
#&gt; SRR1975461     1  0.0424      0.851 0.992 0.000 0.008
#&gt; SRR1975462     1  0.0424      0.851 0.992 0.000 0.008
#&gt; SRR1975459     2  0.0237      0.930 0.004 0.996 0.000
#&gt; SRR1975460     2  0.0237      0.930 0.004 0.996 0.000
#&gt; SRR1975457     1  0.6309     -0.340 0.504 0.000 0.496
#&gt; SRR1975458     1  0.6309     -0.340 0.504 0.000 0.496
#&gt; SRR1975455     3  0.6286      0.376 0.464 0.000 0.536
#&gt; SRR1975456     3  0.6286      0.376 0.464 0.000 0.536
#&gt; SRR1975453     1  0.0424      0.851 0.992 0.000 0.008
#&gt; SRR1975454     1  0.0424      0.851 0.992 0.000 0.008
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-2-a').click(function(){
  $('#tab-SD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-3'>
<p><a id='tab-SD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.0188      0.987 0.000 0.000 0.996 0.004
#&gt; SRR1975507     3  0.0188      0.987 0.000 0.000 0.996 0.004
#&gt; SRR1975506     3  0.0188      0.987 0.000 0.000 0.996 0.004
#&gt; SRR1975505     3  0.0188      0.987 0.000 0.000 0.996 0.004
#&gt; SRR1975503     2  0.2651      0.894 0.096 0.896 0.004 0.004
#&gt; SRR1975504     2  0.2651      0.894 0.096 0.896 0.004 0.004
#&gt; SRR1975501     1  0.3266      0.800 0.832 0.168 0.000 0.000
#&gt; SRR1975502     1  0.3266      0.800 0.832 0.168 0.000 0.000
#&gt; SRR1975499     2  0.3403      0.877 0.112 0.864 0.004 0.020
#&gt; SRR1975500     2  0.3403      0.877 0.112 0.864 0.004 0.020
#&gt; SRR1975497     1  0.2924      0.943 0.884 0.016 0.100 0.000
#&gt; SRR1975498     1  0.2924      0.943 0.884 0.016 0.100 0.000
#&gt; SRR1975493     2  0.0336      0.921 0.008 0.992 0.000 0.000
#&gt; SRR1975494     2  0.0336      0.921 0.008 0.992 0.000 0.000
#&gt; SRR1975495     1  0.2647      0.954 0.880 0.000 0.120 0.000
#&gt; SRR1975496     1  0.2647      0.954 0.880 0.000 0.120 0.000
#&gt; SRR1975491     2  0.0921      0.914 0.028 0.972 0.000 0.000
#&gt; SRR1975492     2  0.1022      0.911 0.032 0.968 0.000 0.000
#&gt; SRR1975489     4  0.0188      0.971 0.000 0.000 0.004 0.996
#&gt; SRR1975490     4  0.0188      0.971 0.000 0.000 0.004 0.996
#&gt; SRR1975487     2  0.6443      0.612 0.112 0.644 0.004 0.240
#&gt; SRR1975488     2  0.6963      0.404 0.112 0.544 0.004 0.340
#&gt; SRR1975485     4  0.0927      0.967 0.008 0.000 0.016 0.976
#&gt; SRR1975486     4  0.0927      0.967 0.008 0.000 0.016 0.976
#&gt; SRR1975483     1  0.2814      0.952 0.868 0.000 0.132 0.000
#&gt; SRR1975484     1  0.2760      0.954 0.872 0.000 0.128 0.000
#&gt; SRR1975481     1  0.2976      0.953 0.872 0.000 0.120 0.008
#&gt; SRR1975482     1  0.2976      0.953 0.872 0.000 0.120 0.008
#&gt; SRR1975477     4  0.1576      0.952 0.004 0.000 0.048 0.948
#&gt; SRR1975478     4  0.1474      0.950 0.000 0.000 0.052 0.948
#&gt; SRR1975479     4  0.0188      0.971 0.000 0.000 0.004 0.996
#&gt; SRR1975480     4  0.0188      0.971 0.000 0.000 0.004 0.996
#&gt; SRR1975475     4  0.3302      0.915 0.096 0.008 0.020 0.876
#&gt; SRR1975476     4  0.3302      0.915 0.096 0.008 0.020 0.876
#&gt; SRR1975473     4  0.0188      0.971 0.000 0.000 0.004 0.996
#&gt; SRR1975474     4  0.0188      0.971 0.000 0.000 0.004 0.996
#&gt; SRR1975471     1  0.2868      0.951 0.864 0.000 0.136 0.000
#&gt; SRR1975472     1  0.2868      0.951 0.864 0.000 0.136 0.000
#&gt; SRR1975469     1  0.2944      0.954 0.868 0.000 0.128 0.004
#&gt; SRR1975470     1  0.2944      0.954 0.868 0.000 0.128 0.004
#&gt; SRR1975467     2  0.1474      0.912 0.052 0.948 0.000 0.000
#&gt; SRR1975468     2  0.1474      0.912 0.052 0.948 0.000 0.000
#&gt; SRR1975465     2  0.0336      0.921 0.008 0.992 0.000 0.000
#&gt; SRR1975466     2  0.0336      0.921 0.008 0.992 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.921 0.000 1.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.921 0.000 1.000 0.000 0.000
#&gt; SRR1975461     3  0.0817      0.976 0.024 0.000 0.976 0.000
#&gt; SRR1975462     3  0.0817      0.976 0.024 0.000 0.976 0.000
#&gt; SRR1975459     2  0.0592      0.919 0.016 0.984 0.000 0.000
#&gt; SRR1975460     2  0.0592      0.919 0.016 0.984 0.000 0.000
#&gt; SRR1975457     3  0.0188      0.987 0.000 0.000 0.996 0.004
#&gt; SRR1975458     3  0.0188      0.987 0.000 0.000 0.996 0.004
#&gt; SRR1975455     3  0.0336      0.984 0.000 0.000 0.992 0.008
#&gt; SRR1975456     3  0.0336      0.984 0.000 0.000 0.992 0.008
#&gt; SRR1975453     3  0.0921      0.973 0.028 0.000 0.972 0.000
#&gt; SRR1975454     3  0.0921      0.973 0.028 0.000 0.972 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-3-a').click(function(){
  $('#tab-SD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-4'>
<p><a id='tab-SD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.1357      0.977 0.048 0.000 0.948 0.000 0.004
#&gt; SRR1975507     3  0.1571      0.980 0.060 0.000 0.936 0.000 0.004
#&gt; SRR1975506     3  0.1571      0.980 0.060 0.000 0.936 0.000 0.004
#&gt; SRR1975505     3  0.1357      0.977 0.048 0.000 0.948 0.000 0.004
#&gt; SRR1975503     2  0.4452     -0.360 0.000 0.500 0.004 0.496 0.000
#&gt; SRR1975504     2  0.4452     -0.360 0.000 0.500 0.004 0.496 0.000
#&gt; SRR1975501     1  0.4731      0.538 0.640 0.328 0.000 0.032 0.000
#&gt; SRR1975502     1  0.4731      0.538 0.640 0.328 0.000 0.032 0.000
#&gt; SRR1975499     4  0.4101      0.603 0.000 0.372 0.000 0.628 0.000
#&gt; SRR1975500     4  0.4101      0.603 0.000 0.372 0.000 0.628 0.000
#&gt; SRR1975497     1  0.1485      0.889 0.948 0.020 0.000 0.032 0.000
#&gt; SRR1975498     1  0.1485      0.889 0.948 0.020 0.000 0.032 0.000
#&gt; SRR1975493     2  0.0404      0.862 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1975494     2  0.0404      0.862 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1975495     1  0.1202      0.895 0.960 0.004 0.004 0.032 0.000
#&gt; SRR1975496     1  0.1202      0.895 0.960 0.004 0.004 0.032 0.000
#&gt; SRR1975491     2  0.1597      0.818 0.048 0.940 0.000 0.012 0.000
#&gt; SRR1975492     2  0.1557      0.815 0.052 0.940 0.000 0.008 0.000
#&gt; SRR1975489     5  0.3010      0.756 0.004 0.000 0.000 0.172 0.824
#&gt; SRR1975490     5  0.3010      0.756 0.004 0.000 0.000 0.172 0.824
#&gt; SRR1975487     4  0.2983      0.692 0.000 0.096 0.000 0.864 0.040
#&gt; SRR1975488     4  0.2903      0.671 0.000 0.080 0.000 0.872 0.048
#&gt; SRR1975485     5  0.4958      0.659 0.000 0.000 0.036 0.372 0.592
#&gt; SRR1975486     5  0.4958      0.659 0.000 0.000 0.036 0.372 0.592
#&gt; SRR1975483     1  0.0290      0.899 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1975484     1  0.0290      0.899 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1975481     1  0.1173      0.895 0.964 0.000 0.004 0.012 0.020
#&gt; SRR1975482     1  0.1173      0.895 0.964 0.000 0.004 0.012 0.020
#&gt; SRR1975477     5  0.2821      0.796 0.012 0.008 0.032 0.052 0.896
#&gt; SRR1975478     5  0.2821      0.796 0.012 0.008 0.032 0.052 0.896
#&gt; SRR1975479     5  0.1041      0.798 0.004 0.000 0.000 0.032 0.964
#&gt; SRR1975480     5  0.1041      0.798 0.004 0.000 0.000 0.032 0.964
#&gt; SRR1975475     5  0.6772      0.609 0.004 0.068 0.076 0.300 0.552
#&gt; SRR1975476     5  0.6757      0.613 0.004 0.068 0.076 0.296 0.556
#&gt; SRR1975473     5  0.1300      0.795 0.028 0.000 0.000 0.016 0.956
#&gt; SRR1975474     5  0.1300      0.795 0.028 0.000 0.000 0.016 0.956
#&gt; SRR1975471     1  0.1740      0.884 0.932 0.000 0.056 0.012 0.000
#&gt; SRR1975472     1  0.1740      0.884 0.932 0.000 0.056 0.012 0.000
#&gt; SRR1975469     1  0.2305      0.881 0.916 0.000 0.044 0.012 0.028
#&gt; SRR1975470     1  0.2305      0.881 0.916 0.000 0.044 0.012 0.028
#&gt; SRR1975467     2  0.1471      0.837 0.004 0.952 0.020 0.024 0.000
#&gt; SRR1975468     2  0.1471      0.837 0.004 0.952 0.020 0.024 0.000
#&gt; SRR1975465     2  0.0162      0.862 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1975466     2  0.0162      0.862 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1975463     2  0.0162      0.862 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1975464     2  0.0162      0.862 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1975461     3  0.1608      0.978 0.072 0.000 0.928 0.000 0.000
#&gt; SRR1975462     3  0.1608      0.978 0.072 0.000 0.928 0.000 0.000
#&gt; SRR1975459     2  0.0609      0.859 0.000 0.980 0.000 0.020 0.000
#&gt; SRR1975460     2  0.0609      0.859 0.000 0.980 0.000 0.020 0.000
#&gt; SRR1975457     3  0.1205      0.972 0.040 0.000 0.956 0.000 0.004
#&gt; SRR1975458     3  0.1205      0.972 0.040 0.000 0.956 0.000 0.004
#&gt; SRR1975455     3  0.2236      0.972 0.068 0.000 0.908 0.000 0.024
#&gt; SRR1975456     3  0.2236      0.972 0.068 0.000 0.908 0.000 0.024
#&gt; SRR1975453     3  0.1732      0.974 0.080 0.000 0.920 0.000 0.000
#&gt; SRR1975454     3  0.1732      0.974 0.080 0.000 0.920 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-4-a').click(function(){
  $('#tab-SD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-5'>
<p><a id='tab-SD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     3  0.0291     0.9869 0.004 0.000 0.992 0.000 0.000 0.004
#&gt; SRR1975507     3  0.0291     0.9869 0.004 0.000 0.992 0.000 0.000 0.004
#&gt; SRR1975506     3  0.0291     0.9869 0.004 0.000 0.992 0.000 0.000 0.004
#&gt; SRR1975505     3  0.0146     0.9855 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1975503     4  0.2996     0.8137 0.000 0.228 0.000 0.772 0.000 0.000
#&gt; SRR1975504     4  0.2996     0.8137 0.000 0.228 0.000 0.772 0.000 0.000
#&gt; SRR1975501     1  0.4697     0.0957 0.528 0.432 0.000 0.004 0.000 0.036
#&gt; SRR1975502     1  0.4697     0.0957 0.528 0.432 0.000 0.004 0.000 0.036
#&gt; SRR1975499     4  0.2613     0.8522 0.000 0.140 0.000 0.848 0.000 0.012
#&gt; SRR1975500     4  0.2613     0.8522 0.000 0.140 0.000 0.848 0.000 0.012
#&gt; SRR1975497     1  0.0777     0.7120 0.972 0.000 0.004 0.000 0.000 0.024
#&gt; SRR1975498     1  0.0777     0.7120 0.972 0.000 0.004 0.000 0.000 0.024
#&gt; SRR1975493     2  0.0692     0.9496 0.000 0.976 0.000 0.004 0.000 0.020
#&gt; SRR1975494     2  0.0692     0.9496 0.000 0.976 0.000 0.004 0.000 0.020
#&gt; SRR1975495     1  0.0653     0.7147 0.980 0.000 0.004 0.004 0.000 0.012
#&gt; SRR1975496     1  0.0653     0.7147 0.980 0.000 0.004 0.004 0.000 0.012
#&gt; SRR1975491     2  0.1922     0.9141 0.040 0.924 0.000 0.012 0.000 0.024
#&gt; SRR1975492     2  0.1890     0.9110 0.044 0.924 0.000 0.008 0.000 0.024
#&gt; SRR1975489     5  0.3735     0.4484 0.000 0.000 0.000 0.092 0.784 0.124
#&gt; SRR1975490     5  0.3735     0.4484 0.000 0.000 0.000 0.092 0.784 0.124
#&gt; SRR1975487     4  0.1367     0.7507 0.000 0.012 0.000 0.944 0.000 0.044
#&gt; SRR1975488     4  0.1434     0.7467 0.000 0.012 0.000 0.940 0.000 0.048
#&gt; SRR1975485     6  0.5715     0.5687 0.000 0.000 0.004 0.144 0.384 0.468
#&gt; SRR1975486     6  0.5715     0.5687 0.000 0.000 0.004 0.144 0.384 0.468
#&gt; SRR1975483     1  0.2520     0.7399 0.844 0.000 0.004 0.000 0.000 0.152
#&gt; SRR1975484     1  0.2520     0.7399 0.844 0.000 0.004 0.000 0.000 0.152
#&gt; SRR1975481     1  0.4191     0.7116 0.704 0.000 0.000 0.000 0.056 0.240
#&gt; SRR1975482     1  0.4191     0.7116 0.704 0.000 0.000 0.000 0.056 0.240
#&gt; SRR1975477     5  0.4794     0.3298 0.008 0.016 0.028 0.000 0.632 0.316
#&gt; SRR1975478     5  0.4794     0.3298 0.008 0.016 0.028 0.000 0.632 0.316
#&gt; SRR1975479     5  0.0000     0.6028 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975480     5  0.0000     0.6028 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975475     6  0.5730     0.5386 0.000 0.028 0.012 0.068 0.332 0.560
#&gt; SRR1975476     6  0.5673     0.5363 0.000 0.024 0.012 0.068 0.336 0.560
#&gt; SRR1975473     5  0.3618     0.5766 0.012 0.008 0.004 0.000 0.764 0.212
#&gt; SRR1975474     5  0.3618     0.5766 0.012 0.008 0.004 0.000 0.764 0.212
#&gt; SRR1975471     1  0.5394     0.6948 0.632 0.000 0.132 0.000 0.020 0.216
#&gt; SRR1975472     1  0.5394     0.6948 0.632 0.000 0.132 0.000 0.020 0.216
#&gt; SRR1975469     1  0.6321     0.6480 0.544 0.000 0.140 0.004 0.052 0.260
#&gt; SRR1975470     1  0.6321     0.6480 0.544 0.000 0.140 0.004 0.052 0.260
#&gt; SRR1975467     2  0.2585     0.8707 0.004 0.880 0.000 0.048 0.000 0.068
#&gt; SRR1975468     2  0.2519     0.8705 0.004 0.884 0.000 0.044 0.000 0.068
#&gt; SRR1975465     2  0.0146     0.9518 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1975466     2  0.0146     0.9518 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1975463     2  0.0260     0.9518 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1975464     2  0.0260     0.9518 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1975461     3  0.0622     0.9825 0.008 0.000 0.980 0.000 0.000 0.012
#&gt; SRR1975462     3  0.0622     0.9825 0.008 0.000 0.980 0.000 0.000 0.012
#&gt; SRR1975459     2  0.0767     0.9471 0.004 0.976 0.000 0.012 0.000 0.008
#&gt; SRR1975460     2  0.0767     0.9471 0.004 0.976 0.000 0.012 0.000 0.008
#&gt; SRR1975457     3  0.0436     0.9859 0.004 0.000 0.988 0.000 0.004 0.004
#&gt; SRR1975458     3  0.0436     0.9859 0.004 0.000 0.988 0.000 0.004 0.004
#&gt; SRR1975455     3  0.0405     0.9847 0.004 0.000 0.988 0.000 0.008 0.000
#&gt; SRR1975456     3  0.0405     0.9847 0.004 0.000 0.988 0.000 0.008 0.000
#&gt; SRR1975453     3  0.0820     0.9779 0.012 0.000 0.972 0.000 0.000 0.016
#&gt; SRR1975454     3  0.0820     0.9779 0.012 0.000 0.972 0.000 0.000 0.016
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-5-a').click(function(){
  $('#tab-SD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-NMF-signature_compare](figure_cola/SD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-SD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-NMF-collect-classes](figure_cola/SD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "hclust"]
# you can also extract it by
# res = res_list["CV:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-hclust-collect-plots](figure_cola/CV-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-hclust-select-partition-number](figure_cola/CV-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.975       0.986          0.156 0.865   0.865
#> 3 3 0.433           0.530       0.785          1.839 0.727   0.685
#> 4 4 0.636           0.731       0.862          0.391 0.675   0.486
#> 5 5 0.776           0.814       0.898          0.123 0.917   0.766
#> 6 6 0.726           0.774       0.835          0.101 0.961   0.862
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-classes'>
<ul>
<li><a href='#tab-CV-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-hclust-get-classes-1'>
<p><a id='tab-CV-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2   0.000      1.000 0.000 1.000
#&gt; SRR1975507     2   0.000      1.000 0.000 1.000
#&gt; SRR1975506     2   0.000      1.000 0.000 1.000
#&gt; SRR1975505     2   0.000      1.000 0.000 1.000
#&gt; SRR1975503     1   0.000      0.985 1.000 0.000
#&gt; SRR1975504     1   0.000      0.985 1.000 0.000
#&gt; SRR1975501     1   0.000      0.985 1.000 0.000
#&gt; SRR1975502     1   0.000      0.985 1.000 0.000
#&gt; SRR1975499     1   0.000      0.985 1.000 0.000
#&gt; SRR1975500     1   0.000      0.985 1.000 0.000
#&gt; SRR1975497     1   0.000      0.985 1.000 0.000
#&gt; SRR1975498     1   0.000      0.985 1.000 0.000
#&gt; SRR1975493     1   0.000      0.985 1.000 0.000
#&gt; SRR1975494     1   0.000      0.985 1.000 0.000
#&gt; SRR1975495     1   0.000      0.985 1.000 0.000
#&gt; SRR1975496     1   0.000      0.985 1.000 0.000
#&gt; SRR1975491     1   0.000      0.985 1.000 0.000
#&gt; SRR1975492     1   0.000      0.985 1.000 0.000
#&gt; SRR1975489     1   0.000      0.985 1.000 0.000
#&gt; SRR1975490     1   0.000      0.985 1.000 0.000
#&gt; SRR1975487     1   0.000      0.985 1.000 0.000
#&gt; SRR1975488     1   0.000      0.985 1.000 0.000
#&gt; SRR1975485     1   0.000      0.985 1.000 0.000
#&gt; SRR1975486     1   0.000      0.985 1.000 0.000
#&gt; SRR1975483     1   0.000      0.985 1.000 0.000
#&gt; SRR1975484     1   0.000      0.985 1.000 0.000
#&gt; SRR1975481     1   0.000      0.985 1.000 0.000
#&gt; SRR1975482     1   0.000      0.985 1.000 0.000
#&gt; SRR1975477     1   0.000      0.985 1.000 0.000
#&gt; SRR1975478     1   0.000      0.985 1.000 0.000
#&gt; SRR1975479     1   0.000      0.985 1.000 0.000
#&gt; SRR1975480     1   0.000      0.985 1.000 0.000
#&gt; SRR1975475     1   0.000      0.985 1.000 0.000
#&gt; SRR1975476     1   0.000      0.985 1.000 0.000
#&gt; SRR1975473     1   0.000      0.985 1.000 0.000
#&gt; SRR1975474     1   0.000      0.985 1.000 0.000
#&gt; SRR1975471     1   0.000      0.985 1.000 0.000
#&gt; SRR1975472     1   0.000      0.985 1.000 0.000
#&gt; SRR1975469     1   0.000      0.985 1.000 0.000
#&gt; SRR1975470     1   0.000      0.985 1.000 0.000
#&gt; SRR1975467     1   0.000      0.985 1.000 0.000
#&gt; SRR1975468     1   0.000      0.985 1.000 0.000
#&gt; SRR1975465     1   0.000      0.985 1.000 0.000
#&gt; SRR1975466     1   0.000      0.985 1.000 0.000
#&gt; SRR1975463     1   0.000      0.985 1.000 0.000
#&gt; SRR1975464     1   0.000      0.985 1.000 0.000
#&gt; SRR1975461     1   0.456      0.908 0.904 0.096
#&gt; SRR1975462     1   0.456      0.908 0.904 0.096
#&gt; SRR1975459     1   0.000      0.985 1.000 0.000
#&gt; SRR1975460     1   0.000      0.985 1.000 0.000
#&gt; SRR1975457     1   0.456      0.908 0.904 0.096
#&gt; SRR1975458     1   0.456      0.908 0.904 0.096
#&gt; SRR1975455     1   0.456      0.908 0.904 0.096
#&gt; SRR1975456     1   0.456      0.908 0.904 0.096
#&gt; SRR1975453     1   0.456      0.908 0.904 0.096
#&gt; SRR1975454     1   0.456      0.908 0.904 0.096
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-1-a').click(function(){
  $('#tab-CV-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-2'>
<p><a id='tab-CV-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975503     1  0.6305     -0.881 0.516 0.484 0.000
#&gt; SRR1975504     1  0.6305     -0.881 0.516 0.484 0.000
#&gt; SRR1975501     1  0.6267     -0.806 0.548 0.452 0.000
#&gt; SRR1975502     1  0.6267     -0.806 0.548 0.452 0.000
#&gt; SRR1975499     1  0.3116      0.503 0.892 0.108 0.000
#&gt; SRR1975500     1  0.3116      0.503 0.892 0.108 0.000
#&gt; SRR1975497     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975493     2  0.6274      0.991 0.456 0.544 0.000
#&gt; SRR1975494     2  0.6274      0.991 0.456 0.544 0.000
#&gt; SRR1975495     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975491     1  0.6291     -0.844 0.532 0.468 0.000
#&gt; SRR1975492     1  0.6291     -0.844 0.532 0.468 0.000
#&gt; SRR1975489     1  0.0424      0.665 0.992 0.008 0.000
#&gt; SRR1975490     1  0.0424      0.665 0.992 0.008 0.000
#&gt; SRR1975487     1  0.0424      0.665 0.992 0.008 0.000
#&gt; SRR1975488     1  0.0424      0.665 0.992 0.008 0.000
#&gt; SRR1975485     1  0.0424      0.665 0.992 0.008 0.000
#&gt; SRR1975486     1  0.0424      0.665 0.992 0.008 0.000
#&gt; SRR1975483     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975477     1  0.4702      0.569 0.788 0.212 0.000
#&gt; SRR1975478     1  0.4702      0.569 0.788 0.212 0.000
#&gt; SRR1975479     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975480     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975475     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975476     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975473     1  0.4702      0.569 0.788 0.212 0.000
#&gt; SRR1975474     1  0.4702      0.569 0.788 0.212 0.000
#&gt; SRR1975471     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.669 1.000 0.000 0.000
#&gt; SRR1975469     1  0.0424      0.665 0.992 0.008 0.000
#&gt; SRR1975470     1  0.0424      0.665 0.992 0.008 0.000
#&gt; SRR1975467     2  0.6299      0.963 0.476 0.524 0.000
#&gt; SRR1975468     2  0.6299      0.963 0.476 0.524 0.000
#&gt; SRR1975465     2  0.6274      0.991 0.456 0.544 0.000
#&gt; SRR1975466     2  0.6274      0.991 0.456 0.544 0.000
#&gt; SRR1975463     2  0.6274      0.991 0.456 0.544 0.000
#&gt; SRR1975464     2  0.6274      0.991 0.456 0.544 0.000
#&gt; SRR1975461     1  0.8524      0.215 0.456 0.452 0.092
#&gt; SRR1975462     1  0.8524      0.215 0.456 0.452 0.092
#&gt; SRR1975459     2  0.6274      0.991 0.456 0.544 0.000
#&gt; SRR1975460     2  0.6274      0.991 0.456 0.544 0.000
#&gt; SRR1975457     1  0.7287      0.514 0.696 0.212 0.092
#&gt; SRR1975458     1  0.7287      0.514 0.696 0.212 0.092
#&gt; SRR1975455     1  0.7287      0.514 0.696 0.212 0.092
#&gt; SRR1975456     1  0.7287      0.514 0.696 0.212 0.092
#&gt; SRR1975453     1  0.8524      0.215 0.456 0.452 0.092
#&gt; SRR1975454     1  0.8524      0.215 0.456 0.452 0.092
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-2-a').click(function(){
  $('#tab-CV-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-3'>
<p><a id='tab-CV-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     4  0.0188      1.000 0.000 0.000 0.004 0.996
#&gt; SRR1975507     4  0.0188      1.000 0.000 0.000 0.004 0.996
#&gt; SRR1975506     4  0.0188      1.000 0.000 0.000 0.004 0.996
#&gt; SRR1975505     4  0.0188      1.000 0.000 0.000 0.004 0.996
#&gt; SRR1975503     2  0.4746      0.647 0.368 0.632 0.000 0.000
#&gt; SRR1975504     2  0.4746      0.647 0.368 0.632 0.000 0.000
#&gt; SRR1975501     2  0.4981      0.495 0.464 0.536 0.000 0.000
#&gt; SRR1975502     2  0.4981      0.495 0.464 0.536 0.000 0.000
#&gt; SRR1975499     1  0.2469      0.780 0.892 0.108 0.000 0.000
#&gt; SRR1975500     1  0.2469      0.780 0.892 0.108 0.000 0.000
#&gt; SRR1975497     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975493     2  0.0000      0.666 0.000 1.000 0.000 0.000
#&gt; SRR1975494     2  0.0000      0.666 0.000 1.000 0.000 0.000
#&gt; SRR1975495     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975491     2  0.4877      0.599 0.408 0.592 0.000 0.000
#&gt; SRR1975492     2  0.4877      0.599 0.408 0.592 0.000 0.000
#&gt; SRR1975489     1  0.0336      0.893 0.992 0.008 0.000 0.000
#&gt; SRR1975490     1  0.0336      0.893 0.992 0.008 0.000 0.000
#&gt; SRR1975487     1  0.0336      0.893 0.992 0.008 0.000 0.000
#&gt; SRR1975488     1  0.0336      0.893 0.992 0.008 0.000 0.000
#&gt; SRR1975485     1  0.0336      0.893 0.992 0.008 0.000 0.000
#&gt; SRR1975486     1  0.0336      0.893 0.992 0.008 0.000 0.000
#&gt; SRR1975483     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975477     1  0.6584      0.114 0.568 0.096 0.336 0.000
#&gt; SRR1975478     1  0.6584      0.114 0.568 0.096 0.336 0.000
#&gt; SRR1975479     1  0.1302      0.861 0.956 0.000 0.044 0.000
#&gt; SRR1975480     1  0.1302      0.861 0.956 0.000 0.044 0.000
#&gt; SRR1975475     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975476     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975473     1  0.6584      0.114 0.568 0.096 0.336 0.000
#&gt; SRR1975474     1  0.6584      0.114 0.568 0.096 0.336 0.000
#&gt; SRR1975471     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.895 1.000 0.000 0.000 0.000
#&gt; SRR1975469     1  0.0336      0.893 0.992 0.008 0.000 0.000
#&gt; SRR1975470     1  0.0336      0.893 0.992 0.008 0.000 0.000
#&gt; SRR1975467     2  0.4543      0.674 0.324 0.676 0.000 0.000
#&gt; SRR1975468     2  0.4543      0.674 0.324 0.676 0.000 0.000
#&gt; SRR1975465     2  0.0188      0.665 0.000 0.996 0.000 0.004
#&gt; SRR1975466     2  0.0188      0.665 0.000 0.996 0.000 0.004
#&gt; SRR1975463     2  0.0188      0.665 0.000 0.996 0.000 0.004
#&gt; SRR1975464     2  0.0188      0.665 0.000 0.996 0.000 0.004
#&gt; SRR1975461     3  0.3144      0.623 0.072 0.000 0.884 0.044
#&gt; SRR1975462     3  0.3144      0.623 0.072 0.000 0.884 0.044
#&gt; SRR1975459     2  0.0188      0.665 0.000 0.996 0.000 0.004
#&gt; SRR1975460     2  0.0188      0.665 0.000 0.996 0.000 0.004
#&gt; SRR1975457     3  0.7767      0.665 0.360 0.096 0.500 0.044
#&gt; SRR1975458     3  0.7767      0.665 0.360 0.096 0.500 0.044
#&gt; SRR1975455     3  0.7767      0.665 0.360 0.096 0.500 0.044
#&gt; SRR1975456     3  0.7767      0.665 0.360 0.096 0.500 0.044
#&gt; SRR1975453     3  0.3144      0.623 0.072 0.000 0.884 0.044
#&gt; SRR1975454     3  0.3144      0.623 0.072 0.000 0.884 0.044
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-3-a').click(function(){
  $('#tab-CV-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-4'>
<p><a id='tab-CV-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975503     2  0.4530      0.616 0.004 0.612  0 0.376 0.008
#&gt; SRR1975504     2  0.4530      0.616 0.004 0.612  0 0.376 0.008
#&gt; SRR1975501     2  0.4700      0.445 0.004 0.516  0 0.472 0.008
#&gt; SRR1975502     2  0.4700      0.445 0.004 0.516  0 0.472 0.008
#&gt; SRR1975499     4  0.2295      0.849 0.004 0.088  0 0.900 0.008
#&gt; SRR1975500     4  0.2295      0.849 0.004 0.088  0 0.900 0.008
#&gt; SRR1975497     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975498     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975493     2  0.0740      0.651 0.004 0.980  0 0.008 0.008
#&gt; SRR1975494     2  0.0740      0.651 0.004 0.980  0 0.008 0.008
#&gt; SRR1975495     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975496     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975491     2  0.4630      0.562 0.004 0.572  0 0.416 0.008
#&gt; SRR1975492     2  0.4630      0.562 0.004 0.572  0 0.416 0.008
#&gt; SRR1975489     4  0.0000      0.965 0.000 0.000  0 1.000 0.000
#&gt; SRR1975490     4  0.0000      0.965 0.000 0.000  0 1.000 0.000
#&gt; SRR1975487     4  0.0000      0.965 0.000 0.000  0 1.000 0.000
#&gt; SRR1975488     4  0.0000      0.965 0.000 0.000  0 1.000 0.000
#&gt; SRR1975485     4  0.0000      0.965 0.000 0.000  0 1.000 0.000
#&gt; SRR1975486     4  0.0000      0.965 0.000 0.000  0 1.000 0.000
#&gt; SRR1975483     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975484     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975481     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975482     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975477     5  0.0404      0.713 0.000 0.000  0 0.012 0.988
#&gt; SRR1975478     5  0.0404      0.713 0.000 0.000  0 0.012 0.988
#&gt; SRR1975479     4  0.2929      0.788 0.000 0.000  0 0.820 0.180
#&gt; SRR1975480     4  0.2929      0.788 0.000 0.000  0 0.820 0.180
#&gt; SRR1975475     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975476     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975473     5  0.0404      0.713 0.000 0.000  0 0.012 0.988
#&gt; SRR1975474     5  0.0404      0.713 0.000 0.000  0 0.012 0.988
#&gt; SRR1975471     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975472     4  0.0290      0.967 0.000 0.000  0 0.992 0.008
#&gt; SRR1975469     4  0.0000      0.965 0.000 0.000  0 1.000 0.000
#&gt; SRR1975470     4  0.0000      0.965 0.000 0.000  0 1.000 0.000
#&gt; SRR1975467     2  0.3949      0.655 0.000 0.668  0 0.332 0.000
#&gt; SRR1975468     2  0.3949      0.655 0.000 0.668  0 0.332 0.000
#&gt; SRR1975465     2  0.0451      0.650 0.008 0.988  0 0.000 0.004
#&gt; SRR1975466     2  0.0451      0.650 0.008 0.988  0 0.000 0.004
#&gt; SRR1975463     2  0.0451      0.650 0.008 0.988  0 0.000 0.004
#&gt; SRR1975464     2  0.0451      0.650 0.008 0.988  0 0.000 0.004
#&gt; SRR1975461     1  0.0404      1.000 0.988 0.000  0 0.012 0.000
#&gt; SRR1975462     1  0.0404      1.000 0.988 0.000  0 0.012 0.000
#&gt; SRR1975459     2  0.0451      0.650 0.008 0.988  0 0.000 0.004
#&gt; SRR1975460     2  0.0451      0.650 0.008 0.988  0 0.000 0.004
#&gt; SRR1975457     5  0.4537      0.599 0.396 0.000  0 0.012 0.592
#&gt; SRR1975458     5  0.4537      0.599 0.396 0.000  0 0.012 0.592
#&gt; SRR1975455     5  0.4537      0.599 0.396 0.000  0 0.012 0.592
#&gt; SRR1975456     5  0.4537      0.599 0.396 0.000  0 0.012 0.592
#&gt; SRR1975453     1  0.0404      1.000 0.988 0.000  0 0.012 0.000
#&gt; SRR1975454     1  0.0404      1.000 0.988 0.000  0 0.012 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-4-a').click(function(){
  $('#tab-CV-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-5'>
<p><a id='tab-CV-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3   p4    p5    p6
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000  1 0.00 0.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000  1 0.00 0.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000  1 0.00 0.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000  1 0.00 0.000 0.000
#&gt; SRR1975503     6  0.3547      0.803 0.300 0.004  0 0.00 0.000 0.696
#&gt; SRR1975504     6  0.3547      0.803 0.300 0.004  0 0.00 0.000 0.696
#&gt; SRR1975501     6  0.3872      0.741 0.392 0.004  0 0.00 0.000 0.604
#&gt; SRR1975502     6  0.3872      0.741 0.392 0.004  0 0.00 0.000 0.604
#&gt; SRR1975499     1  0.2454      0.619 0.840 0.000  0 0.00 0.000 0.160
#&gt; SRR1975500     1  0.2454      0.619 0.840 0.000  0 0.00 0.000 0.160
#&gt; SRR1975497     1  0.0547      0.790 0.980 0.000  0 0.00 0.000 0.020
#&gt; SRR1975498     1  0.0547      0.790 0.980 0.000  0 0.00 0.000 0.020
#&gt; SRR1975493     6  0.3684      0.159 0.000 0.372  0 0.00 0.000 0.628
#&gt; SRR1975494     6  0.3684      0.159 0.000 0.372  0 0.00 0.000 0.628
#&gt; SRR1975495     1  0.3409      0.703 0.700 0.000  0 0.00 0.000 0.300
#&gt; SRR1975496     1  0.3409      0.703 0.700 0.000  0 0.00 0.000 0.300
#&gt; SRR1975491     6  0.3714      0.803 0.340 0.004  0 0.00 0.000 0.656
#&gt; SRR1975492     6  0.3714      0.803 0.340 0.004  0 0.00 0.000 0.656
#&gt; SRR1975489     1  0.0260      0.790 0.992 0.000  0 0.00 0.000 0.008
#&gt; SRR1975490     1  0.0260      0.790 0.992 0.000  0 0.00 0.000 0.008
#&gt; SRR1975487     1  0.0865      0.779 0.964 0.000  0 0.00 0.000 0.036
#&gt; SRR1975488     1  0.0865      0.779 0.964 0.000  0 0.00 0.000 0.036
#&gt; SRR1975485     1  0.0790      0.782 0.968 0.000  0 0.00 0.000 0.032
#&gt; SRR1975486     1  0.0790      0.782 0.968 0.000  0 0.00 0.000 0.032
#&gt; SRR1975483     1  0.3409      0.703 0.700 0.000  0 0.00 0.000 0.300
#&gt; SRR1975484     1  0.3409      0.703 0.700 0.000  0 0.00 0.000 0.300
#&gt; SRR1975481     1  0.3409      0.703 0.700 0.000  0 0.00 0.000 0.300
#&gt; SRR1975482     1  0.3409      0.703 0.700 0.000  0 0.00 0.000 0.300
#&gt; SRR1975477     5  0.0000      0.705 0.000 0.000  0 0.00 1.000 0.000
#&gt; SRR1975478     5  0.0000      0.705 0.000 0.000  0 0.00 1.000 0.000
#&gt; SRR1975479     1  0.2631      0.639 0.820 0.000  0 0.00 0.180 0.000
#&gt; SRR1975480     1  0.2631      0.639 0.820 0.000  0 0.00 0.180 0.000
#&gt; SRR1975475     1  0.0000      0.792 1.000 0.000  0 0.00 0.000 0.000
#&gt; SRR1975476     1  0.0000      0.792 1.000 0.000  0 0.00 0.000 0.000
#&gt; SRR1975473     5  0.0000      0.705 0.000 0.000  0 0.00 1.000 0.000
#&gt; SRR1975474     5  0.0000      0.705 0.000 0.000  0 0.00 1.000 0.000
#&gt; SRR1975471     1  0.3409      0.703 0.700 0.000  0 0.00 0.000 0.300
#&gt; SRR1975472     1  0.3409      0.703 0.700 0.000  0 0.00 0.000 0.300
#&gt; SRR1975469     1  0.1141      0.789 0.948 0.000  0 0.00 0.000 0.052
#&gt; SRR1975470     1  0.1141      0.789 0.948 0.000  0 0.00 0.000 0.052
#&gt; SRR1975467     6  0.5100      0.761 0.284 0.116  0 0.00 0.000 0.600
#&gt; SRR1975468     6  0.5100      0.761 0.284 0.116  0 0.00 0.000 0.600
#&gt; SRR1975465     2  0.1610      1.000 0.000 0.916  0 0.00 0.000 0.084
#&gt; SRR1975466     2  0.1610      1.000 0.000 0.916  0 0.00 0.000 0.084
#&gt; SRR1975463     2  0.1610      1.000 0.000 0.916  0 0.00 0.000 0.084
#&gt; SRR1975464     2  0.1610      1.000 0.000 0.916  0 0.00 0.000 0.084
#&gt; SRR1975461     4  0.0000      1.000 0.000 0.000  0 1.00 0.000 0.000
#&gt; SRR1975462     4  0.0000      1.000 0.000 0.000  0 1.00 0.000 0.000
#&gt; SRR1975459     2  0.1610      1.000 0.000 0.916  0 0.00 0.000 0.084
#&gt; SRR1975460     2  0.1610      1.000 0.000 0.916  0 0.00 0.000 0.084
#&gt; SRR1975457     5  0.5168      0.601 0.000 0.084  0 0.36 0.552 0.004
#&gt; SRR1975458     5  0.5168      0.601 0.000 0.084  0 0.36 0.552 0.004
#&gt; SRR1975455     5  0.5168      0.601 0.000 0.084  0 0.36 0.552 0.004
#&gt; SRR1975456     5  0.5168      0.601 0.000 0.084  0 0.36 0.552 0.004
#&gt; SRR1975453     4  0.0000      1.000 0.000 0.000  0 1.00 0.000 0.000
#&gt; SRR1975454     4  0.0000      1.000 0.000 0.000  0 1.00 0.000 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-5-a').click(function(){
  $('#tab-CV-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-hclust-signature_compare](figure_cola/CV-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-hclust-collect-classes](figure_cola/CV-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "kmeans"]
# you can also extract it by
# res = res_list["CV:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-kmeans-collect-plots](figure_cola/CV-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-kmeans-select-partition-number](figure_cola/CV-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.419           0.860       0.879         0.3448 0.618   0.618
#> 3 3 0.433           0.671       0.783         0.5894 0.735   0.598
#> 4 4 0.433           0.629       0.692         0.2055 0.883   0.741
#> 5 5 0.500           0.529       0.695         0.0960 0.974   0.928
#> 6 6 0.553           0.560       0.668         0.0629 0.925   0.793
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-classes'>
<ul>
<li><a href='#tab-CV-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-kmeans-get-classes-1'>
<p><a id='tab-CV-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.3274      0.823 0.060 0.940
#&gt; SRR1975507     2  0.3274      0.823 0.060 0.940
#&gt; SRR1975506     2  0.3274      0.823 0.060 0.940
#&gt; SRR1975505     2  0.3274      0.823 0.060 0.940
#&gt; SRR1975503     1  0.0376      0.879 0.996 0.004
#&gt; SRR1975504     1  0.0376      0.879 0.996 0.004
#&gt; SRR1975501     1  0.0376      0.879 0.996 0.004
#&gt; SRR1975502     1  0.0376      0.879 0.996 0.004
#&gt; SRR1975499     1  0.2603      0.894 0.956 0.044
#&gt; SRR1975500     1  0.2603      0.894 0.956 0.044
#&gt; SRR1975497     1  0.5294      0.902 0.880 0.120
#&gt; SRR1975498     1  0.5294      0.902 0.880 0.120
#&gt; SRR1975493     1  0.2948      0.847 0.948 0.052
#&gt; SRR1975494     1  0.2948      0.847 0.948 0.052
#&gt; SRR1975495     1  0.5408      0.902 0.876 0.124
#&gt; SRR1975496     1  0.5408      0.902 0.876 0.124
#&gt; SRR1975491     1  0.0376      0.879 0.996 0.004
#&gt; SRR1975492     1  0.0376      0.879 0.996 0.004
#&gt; SRR1975489     1  0.5408      0.902 0.876 0.124
#&gt; SRR1975490     1  0.5408      0.902 0.876 0.124
#&gt; SRR1975487     1  0.3584      0.899 0.932 0.068
#&gt; SRR1975488     1  0.3584      0.899 0.932 0.068
#&gt; SRR1975485     1  0.5294      0.902 0.880 0.120
#&gt; SRR1975486     1  0.5294      0.902 0.880 0.120
#&gt; SRR1975483     1  0.5294      0.902 0.880 0.120
#&gt; SRR1975484     1  0.5294      0.902 0.880 0.120
#&gt; SRR1975481     1  0.5408      0.902 0.876 0.124
#&gt; SRR1975482     1  0.5408      0.902 0.876 0.124
#&gt; SRR1975477     2  0.9635      0.577 0.388 0.612
#&gt; SRR1975478     2  0.9635      0.577 0.388 0.612
#&gt; SRR1975479     1  0.5519      0.900 0.872 0.128
#&gt; SRR1975480     1  0.5519      0.900 0.872 0.128
#&gt; SRR1975475     1  0.5294      0.902 0.880 0.120
#&gt; SRR1975476     1  0.5294      0.902 0.880 0.120
#&gt; SRR1975473     1  0.5946      0.889 0.856 0.144
#&gt; SRR1975474     1  0.5946      0.889 0.856 0.144
#&gt; SRR1975471     1  0.5408      0.902 0.876 0.124
#&gt; SRR1975472     1  0.5408      0.902 0.876 0.124
#&gt; SRR1975469     1  0.5294      0.902 0.880 0.120
#&gt; SRR1975470     1  0.5294      0.902 0.880 0.120
#&gt; SRR1975467     1  0.2948      0.847 0.948 0.052
#&gt; SRR1975468     1  0.2948      0.847 0.948 0.052
#&gt; SRR1975465     1  0.4022      0.834 0.920 0.080
#&gt; SRR1975466     1  0.4022      0.834 0.920 0.080
#&gt; SRR1975463     1  0.3431      0.843 0.936 0.064
#&gt; SRR1975464     1  0.3431      0.843 0.936 0.064
#&gt; SRR1975461     2  0.4161      0.832 0.084 0.916
#&gt; SRR1975462     2  0.4161      0.832 0.084 0.916
#&gt; SRR1975459     1  0.4022      0.834 0.920 0.080
#&gt; SRR1975460     1  0.4022      0.834 0.920 0.080
#&gt; SRR1975457     2  0.8081      0.829 0.248 0.752
#&gt; SRR1975458     2  0.8081      0.829 0.248 0.752
#&gt; SRR1975455     2  0.8081      0.831 0.248 0.752
#&gt; SRR1975456     2  0.8081      0.831 0.248 0.752
#&gt; SRR1975453     2  0.7950      0.834 0.240 0.760
#&gt; SRR1975454     2  0.7950      0.834 0.240 0.760
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-1-a').click(function(){
  $('#tab-CV-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-2'>
<p><a id='tab-CV-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.2443      0.717 0.032 0.028 0.940
#&gt; SRR1975507     3  0.2443      0.717 0.032 0.028 0.940
#&gt; SRR1975506     3  0.2443      0.717 0.032 0.028 0.940
#&gt; SRR1975505     3  0.2443      0.717 0.032 0.028 0.940
#&gt; SRR1975503     1  0.5678      0.280 0.684 0.316 0.000
#&gt; SRR1975504     1  0.5678      0.280 0.684 0.316 0.000
#&gt; SRR1975501     1  0.5591      0.290 0.696 0.304 0.000
#&gt; SRR1975502     1  0.5591      0.290 0.696 0.304 0.000
#&gt; SRR1975499     1  0.3482      0.673 0.872 0.128 0.000
#&gt; SRR1975500     1  0.3482      0.673 0.872 0.128 0.000
#&gt; SRR1975497     1  0.0237      0.765 0.996 0.004 0.000
#&gt; SRR1975498     1  0.0237      0.765 0.996 0.004 0.000
#&gt; SRR1975493     2  0.5785      0.916 0.300 0.696 0.004
#&gt; SRR1975494     2  0.5785      0.916 0.300 0.696 0.004
#&gt; SRR1975495     1  0.2063      0.753 0.948 0.044 0.008
#&gt; SRR1975496     1  0.2063      0.753 0.948 0.044 0.008
#&gt; SRR1975491     1  0.5678      0.280 0.684 0.316 0.000
#&gt; SRR1975492     1  0.5678      0.280 0.684 0.316 0.000
#&gt; SRR1975489     1  0.1647      0.761 0.960 0.036 0.004
#&gt; SRR1975490     1  0.1647      0.761 0.960 0.036 0.004
#&gt; SRR1975487     1  0.2537      0.730 0.920 0.080 0.000
#&gt; SRR1975488     1  0.2537      0.730 0.920 0.080 0.000
#&gt; SRR1975485     1  0.1411      0.761 0.964 0.036 0.000
#&gt; SRR1975486     1  0.1411      0.761 0.964 0.036 0.000
#&gt; SRR1975483     1  0.1399      0.761 0.968 0.028 0.004
#&gt; SRR1975484     1  0.1399      0.761 0.968 0.028 0.004
#&gt; SRR1975481     1  0.1765      0.757 0.956 0.040 0.004
#&gt; SRR1975482     1  0.1765      0.757 0.956 0.040 0.004
#&gt; SRR1975477     1  0.9852     -0.326 0.416 0.272 0.312
#&gt; SRR1975478     1  0.9852     -0.326 0.416 0.272 0.312
#&gt; SRR1975479     1  0.2550      0.756 0.932 0.056 0.012
#&gt; SRR1975480     1  0.2550      0.756 0.932 0.056 0.012
#&gt; SRR1975475     1  0.1647      0.761 0.960 0.036 0.004
#&gt; SRR1975476     1  0.1647      0.761 0.960 0.036 0.004
#&gt; SRR1975473     1  0.6771      0.508 0.684 0.276 0.040
#&gt; SRR1975474     1  0.6771      0.508 0.684 0.276 0.040
#&gt; SRR1975471     1  0.5756      0.562 0.764 0.208 0.028
#&gt; SRR1975472     1  0.5756      0.562 0.764 0.208 0.028
#&gt; SRR1975469     1  0.0237      0.766 0.996 0.004 0.000
#&gt; SRR1975470     1  0.0237      0.766 0.996 0.004 0.000
#&gt; SRR1975467     2  0.6062      0.803 0.384 0.616 0.000
#&gt; SRR1975468     2  0.6062      0.803 0.384 0.616 0.000
#&gt; SRR1975465     2  0.5812      0.937 0.264 0.724 0.012
#&gt; SRR1975466     2  0.5812      0.937 0.264 0.724 0.012
#&gt; SRR1975463     2  0.5812      0.937 0.264 0.724 0.012
#&gt; SRR1975464     2  0.5812      0.937 0.264 0.724 0.012
#&gt; SRR1975461     3  0.6034      0.764 0.068 0.152 0.780
#&gt; SRR1975462     3  0.6034      0.764 0.068 0.152 0.780
#&gt; SRR1975459     2  0.5775      0.934 0.260 0.728 0.012
#&gt; SRR1975460     2  0.5775      0.934 0.260 0.728 0.012
#&gt; SRR1975457     3  0.9181      0.751 0.236 0.224 0.540
#&gt; SRR1975458     3  0.9181      0.751 0.236 0.224 0.540
#&gt; SRR1975455     3  0.9148      0.751 0.236 0.220 0.544
#&gt; SRR1975456     3  0.9148      0.751 0.236 0.220 0.544
#&gt; SRR1975453     3  0.9468      0.713 0.276 0.228 0.496
#&gt; SRR1975454     3  0.9468      0.713 0.276 0.228 0.496
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-2-a').click(function(){
  $('#tab-CV-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-3'>
<p><a id='tab-CV-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     4  0.0524      0.835 0.004 0.008 0.000 0.988
#&gt; SRR1975507     4  0.0524      0.835 0.004 0.008 0.000 0.988
#&gt; SRR1975506     4  0.0524      0.835 0.004 0.008 0.000 0.988
#&gt; SRR1975505     4  0.0524      0.835 0.004 0.008 0.000 0.988
#&gt; SRR1975503     1  0.6521      0.483 0.620 0.256 0.124 0.000
#&gt; SRR1975504     1  0.6521      0.483 0.620 0.256 0.124 0.000
#&gt; SRR1975501     1  0.6781      0.485 0.596 0.256 0.148 0.000
#&gt; SRR1975502     1  0.6781      0.485 0.596 0.256 0.148 0.000
#&gt; SRR1975499     1  0.4477      0.712 0.808 0.084 0.108 0.000
#&gt; SRR1975500     1  0.4477      0.712 0.808 0.084 0.108 0.000
#&gt; SRR1975497     1  0.2450      0.724 0.912 0.016 0.072 0.000
#&gt; SRR1975498     1  0.2450      0.724 0.912 0.016 0.072 0.000
#&gt; SRR1975493     2  0.4168      0.879 0.092 0.828 0.080 0.000
#&gt; SRR1975494     2  0.4168      0.879 0.092 0.828 0.080 0.000
#&gt; SRR1975495     1  0.4011      0.616 0.784 0.000 0.208 0.008
#&gt; SRR1975496     1  0.4011      0.616 0.784 0.000 0.208 0.008
#&gt; SRR1975491     1  0.6656      0.487 0.608 0.256 0.136 0.000
#&gt; SRR1975492     1  0.6656      0.487 0.608 0.256 0.136 0.000
#&gt; SRR1975489     1  0.3037      0.737 0.888 0.076 0.036 0.000
#&gt; SRR1975490     1  0.3037      0.737 0.888 0.076 0.036 0.000
#&gt; SRR1975487     1  0.4344      0.718 0.816 0.076 0.108 0.000
#&gt; SRR1975488     1  0.4344      0.718 0.816 0.076 0.108 0.000
#&gt; SRR1975485     1  0.2773      0.739 0.900 0.072 0.028 0.000
#&gt; SRR1975486     1  0.2773      0.739 0.900 0.072 0.028 0.000
#&gt; SRR1975483     1  0.3852      0.626 0.808 0.000 0.180 0.012
#&gt; SRR1975484     1  0.3852      0.626 0.808 0.000 0.180 0.012
#&gt; SRR1975481     1  0.3937      0.621 0.800 0.000 0.188 0.012
#&gt; SRR1975482     1  0.3937      0.621 0.800 0.000 0.188 0.012
#&gt; SRR1975477     3  0.7650      0.501 0.228 0.048 0.592 0.132
#&gt; SRR1975478     3  0.7650      0.501 0.228 0.048 0.592 0.132
#&gt; SRR1975479     1  0.4789      0.620 0.772 0.056 0.172 0.000
#&gt; SRR1975480     1  0.4789      0.620 0.772 0.056 0.172 0.000
#&gt; SRR1975475     1  0.3471      0.738 0.868 0.072 0.060 0.000
#&gt; SRR1975476     1  0.3471      0.738 0.868 0.072 0.060 0.000
#&gt; SRR1975473     3  0.6272      0.303 0.392 0.044 0.556 0.008
#&gt; SRR1975474     3  0.6272      0.303 0.392 0.044 0.556 0.008
#&gt; SRR1975471     1  0.5323      0.205 0.592 0.004 0.396 0.008
#&gt; SRR1975472     1  0.5323      0.205 0.592 0.004 0.396 0.008
#&gt; SRR1975469     1  0.1474      0.716 0.948 0.000 0.052 0.000
#&gt; SRR1975470     1  0.1474      0.716 0.948 0.000 0.052 0.000
#&gt; SRR1975467     2  0.5956      0.719 0.220 0.680 0.100 0.000
#&gt; SRR1975468     2  0.5956      0.719 0.220 0.680 0.100 0.000
#&gt; SRR1975465     2  0.2596      0.904 0.068 0.908 0.024 0.000
#&gt; SRR1975466     2  0.2596      0.904 0.068 0.908 0.024 0.000
#&gt; SRR1975463     2  0.2124      0.903 0.068 0.924 0.008 0.000
#&gt; SRR1975464     2  0.2124      0.903 0.068 0.924 0.008 0.000
#&gt; SRR1975461     4  0.5724      0.568 0.024 0.032 0.244 0.700
#&gt; SRR1975462     4  0.5724      0.568 0.024 0.032 0.244 0.700
#&gt; SRR1975459     2  0.2699      0.904 0.068 0.904 0.028 0.000
#&gt; SRR1975460     2  0.2699      0.904 0.068 0.904 0.028 0.000
#&gt; SRR1975457     3  0.7384      0.344 0.104 0.016 0.452 0.428
#&gt; SRR1975458     3  0.7384      0.344 0.104 0.016 0.452 0.428
#&gt; SRR1975455     3  0.7193      0.355 0.096 0.012 0.468 0.424
#&gt; SRR1975456     3  0.7193      0.355 0.096 0.012 0.468 0.424
#&gt; SRR1975453     3  0.8365      0.331 0.192 0.032 0.416 0.360
#&gt; SRR1975454     3  0.8365      0.331 0.192 0.032 0.416 0.360
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-3-a').click(function(){
  $('#tab-CV-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-4'>
<p><a id='tab-CV-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.0162     0.5547 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975507     3  0.0162     0.5547 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975506     3  0.0671     0.5547 0.016 0.004 0.980 0.000 0.000
#&gt; SRR1975505     3  0.0671     0.5547 0.016 0.004 0.980 0.000 0.000
#&gt; SRR1975503     4  0.5924     0.4732 0.280 0.116 0.000 0.596 0.008
#&gt; SRR1975504     4  0.5924     0.4732 0.280 0.116 0.000 0.596 0.008
#&gt; SRR1975501     4  0.6059     0.5224 0.268 0.136 0.000 0.588 0.008
#&gt; SRR1975502     4  0.6059     0.5224 0.268 0.136 0.000 0.588 0.008
#&gt; SRR1975499     4  0.3170     0.6725 0.160 0.004 0.000 0.828 0.008
#&gt; SRR1975500     4  0.3170     0.6725 0.160 0.004 0.000 0.828 0.008
#&gt; SRR1975497     4  0.2900     0.6908 0.108 0.000 0.000 0.864 0.028
#&gt; SRR1975498     4  0.2900     0.6908 0.108 0.000 0.000 0.864 0.028
#&gt; SRR1975493     2  0.5585     0.7405 0.256 0.656 0.000 0.052 0.036
#&gt; SRR1975494     2  0.5585     0.7405 0.256 0.656 0.000 0.052 0.036
#&gt; SRR1975495     4  0.5971     0.4974 0.240 0.004 0.000 0.600 0.156
#&gt; SRR1975496     4  0.5971     0.4974 0.240 0.004 0.000 0.600 0.156
#&gt; SRR1975491     4  0.6280     0.5046 0.288 0.120 0.000 0.572 0.020
#&gt; SRR1975492     4  0.6280     0.5046 0.288 0.120 0.000 0.572 0.020
#&gt; SRR1975489     4  0.1280     0.6969 0.008 0.008 0.000 0.960 0.024
#&gt; SRR1975490     4  0.1280     0.6969 0.008 0.008 0.000 0.960 0.024
#&gt; SRR1975487     4  0.3087     0.6746 0.152 0.004 0.000 0.836 0.008
#&gt; SRR1975488     4  0.3087     0.6746 0.152 0.004 0.000 0.836 0.008
#&gt; SRR1975485     4  0.0854     0.6997 0.012 0.004 0.000 0.976 0.008
#&gt; SRR1975486     4  0.0854     0.6997 0.012 0.004 0.000 0.976 0.008
#&gt; SRR1975483     4  0.5726     0.5315 0.212 0.004 0.000 0.636 0.148
#&gt; SRR1975484     4  0.5726     0.5315 0.212 0.004 0.000 0.636 0.148
#&gt; SRR1975481     4  0.5747     0.5338 0.200 0.004 0.000 0.636 0.160
#&gt; SRR1975482     4  0.5747     0.5338 0.200 0.004 0.000 0.636 0.160
#&gt; SRR1975477     5  0.4522     0.5115 0.016 0.008 0.084 0.100 0.792
#&gt; SRR1975478     5  0.4522     0.5115 0.016 0.008 0.084 0.100 0.792
#&gt; SRR1975479     4  0.4288     0.5663 0.032 0.004 0.000 0.740 0.224
#&gt; SRR1975480     4  0.4288     0.5663 0.032 0.004 0.000 0.740 0.224
#&gt; SRR1975475     4  0.2547     0.6912 0.040 0.004 0.004 0.904 0.048
#&gt; SRR1975476     4  0.2547     0.6912 0.040 0.004 0.004 0.904 0.048
#&gt; SRR1975473     5  0.4448     0.4945 0.012 0.008 0.016 0.224 0.740
#&gt; SRR1975474     5  0.4448     0.4945 0.012 0.008 0.016 0.224 0.740
#&gt; SRR1975471     4  0.6794    -0.0837 0.300 0.000 0.000 0.380 0.320
#&gt; SRR1975472     4  0.6794    -0.0837 0.300 0.000 0.000 0.380 0.320
#&gt; SRR1975469     4  0.2423     0.6917 0.080 0.000 0.000 0.896 0.024
#&gt; SRR1975470     4  0.2423     0.6917 0.080 0.000 0.000 0.896 0.024
#&gt; SRR1975467     2  0.6553     0.5743 0.272 0.520 0.000 0.200 0.008
#&gt; SRR1975468     2  0.6553     0.5743 0.272 0.520 0.000 0.200 0.008
#&gt; SRR1975465     2  0.1820     0.8140 0.020 0.940 0.000 0.020 0.020
#&gt; SRR1975466     2  0.1820     0.8140 0.020 0.940 0.000 0.020 0.020
#&gt; SRR1975463     2  0.1560     0.8188 0.028 0.948 0.000 0.020 0.004
#&gt; SRR1975464     2  0.1560     0.8188 0.028 0.948 0.000 0.020 0.004
#&gt; SRR1975461     3  0.6372     0.0515 0.260 0.000 0.552 0.008 0.180
#&gt; SRR1975462     3  0.6372     0.0515 0.260 0.000 0.552 0.008 0.180
#&gt; SRR1975459     2  0.1173     0.8177 0.004 0.964 0.000 0.020 0.012
#&gt; SRR1975460     2  0.1173     0.8177 0.004 0.964 0.000 0.020 0.012
#&gt; SRR1975457     3  0.7645    -0.2296 0.184 0.004 0.380 0.056 0.376
#&gt; SRR1975458     3  0.7645    -0.2296 0.184 0.004 0.380 0.056 0.376
#&gt; SRR1975455     5  0.7309    -0.2402 0.136 0.004 0.368 0.052 0.440
#&gt; SRR1975456     5  0.7309    -0.2402 0.136 0.004 0.368 0.052 0.440
#&gt; SRR1975453     1  0.8091     1.0000 0.380 0.000 0.260 0.104 0.256
#&gt; SRR1975454     1  0.8091     1.0000 0.380 0.000 0.260 0.104 0.256
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-4-a').click(function(){
  $('#tab-CV-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-5'>
<p><a id='tab-CV-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR1975508     3  0.3973     0.9926 0.296 0.000 0.684 0.000 0.008 NA
#&gt; SRR1975507     3  0.3973     0.9926 0.296 0.000 0.684 0.000 0.012 NA
#&gt; SRR1975506     3  0.3634     0.9934 0.296 0.000 0.696 0.000 0.008 NA
#&gt; SRR1975505     3  0.3634     0.9934 0.296 0.000 0.696 0.000 0.008 NA
#&gt; SRR1975503     4  0.6256     0.4085 0.004 0.100 0.016 0.504 0.024 NA
#&gt; SRR1975504     4  0.6256     0.4085 0.004 0.100 0.016 0.504 0.024 NA
#&gt; SRR1975501     4  0.7100     0.4211 0.016 0.128 0.024 0.456 0.040 NA
#&gt; SRR1975502     4  0.7100     0.4211 0.016 0.128 0.024 0.456 0.040 NA
#&gt; SRR1975499     4  0.3804     0.6038 0.000 0.012 0.016 0.756 0.004 NA
#&gt; SRR1975500     4  0.3804     0.6038 0.000 0.012 0.016 0.756 0.004 NA
#&gt; SRR1975497     4  0.4260     0.5936 0.028 0.000 0.008 0.772 0.048 NA
#&gt; SRR1975498     4  0.4260     0.5936 0.028 0.000 0.008 0.772 0.048 NA
#&gt; SRR1975493     2  0.6336     0.6818 0.004 0.564 0.052 0.024 0.072 NA
#&gt; SRR1975494     2  0.6336     0.6818 0.004 0.564 0.052 0.024 0.072 NA
#&gt; SRR1975495     4  0.7682     0.3627 0.100 0.000 0.076 0.480 0.136 NA
#&gt; SRR1975496     4  0.7682     0.3627 0.100 0.000 0.076 0.480 0.136 NA
#&gt; SRR1975491     4  0.6843     0.3842 0.012 0.124 0.032 0.456 0.020 NA
#&gt; SRR1975492     4  0.6843     0.3842 0.012 0.124 0.032 0.456 0.020 NA
#&gt; SRR1975489     4  0.2327     0.6192 0.000 0.012 0.008 0.908 0.028 NA
#&gt; SRR1975490     4  0.2327     0.6192 0.000 0.012 0.008 0.908 0.028 NA
#&gt; SRR1975487     4  0.3338     0.6144 0.000 0.012 0.004 0.800 0.008 NA
#&gt; SRR1975488     4  0.3338     0.6144 0.000 0.012 0.004 0.800 0.008 NA
#&gt; SRR1975485     4  0.1476     0.6282 0.004 0.012 0.008 0.948 0.000 NA
#&gt; SRR1975486     4  0.1476     0.6282 0.004 0.012 0.008 0.948 0.000 NA
#&gt; SRR1975483     4  0.7645     0.3400 0.100 0.004 0.052 0.476 0.232 NA
#&gt; SRR1975484     4  0.7645     0.3400 0.100 0.004 0.052 0.476 0.232 NA
#&gt; SRR1975481     4  0.7509     0.3348 0.092 0.004 0.048 0.488 0.236 NA
#&gt; SRR1975482     4  0.7509     0.3348 0.092 0.004 0.048 0.488 0.236 NA
#&gt; SRR1975477     5  0.5538     0.7717 0.200 0.004 0.032 0.052 0.676 NA
#&gt; SRR1975478     5  0.5471     0.7717 0.200 0.004 0.032 0.052 0.680 NA
#&gt; SRR1975479     4  0.5171     0.3670 0.012 0.008 0.020 0.664 0.252 NA
#&gt; SRR1975480     4  0.5171     0.3670 0.012 0.008 0.020 0.664 0.252 NA
#&gt; SRR1975475     4  0.3413     0.5982 0.008 0.012 0.012 0.852 0.056 NA
#&gt; SRR1975476     4  0.3413     0.5982 0.008 0.012 0.012 0.852 0.056 NA
#&gt; SRR1975473     5  0.5360     0.7951 0.100 0.004 0.012 0.176 0.684 NA
#&gt; SRR1975474     5  0.5360     0.7951 0.100 0.004 0.012 0.176 0.684 NA
#&gt; SRR1975471     1  0.8255    -0.0373 0.296 0.000 0.048 0.276 0.240 NA
#&gt; SRR1975472     1  0.8255    -0.0373 0.296 0.000 0.048 0.276 0.240 NA
#&gt; SRR1975469     4  0.3515     0.6038 0.024 0.000 0.000 0.828 0.064 NA
#&gt; SRR1975470     4  0.3515     0.6038 0.024 0.000 0.000 0.828 0.064 NA
#&gt; SRR1975467     2  0.6176     0.5896 0.004 0.480 0.016 0.112 0.012 NA
#&gt; SRR1975468     2  0.6176     0.5896 0.004 0.480 0.016 0.112 0.012 NA
#&gt; SRR1975465     2  0.1590     0.7844 0.000 0.944 0.028 0.008 0.012 NA
#&gt; SRR1975466     2  0.1590     0.7844 0.000 0.944 0.028 0.008 0.012 NA
#&gt; SRR1975463     2  0.2407     0.7852 0.000 0.904 0.036 0.008 0.012 NA
#&gt; SRR1975464     2  0.2407     0.7852 0.000 0.904 0.036 0.008 0.012 NA
#&gt; SRR1975461     1  0.3122     0.2765 0.816 0.000 0.160 0.020 0.000 NA
#&gt; SRR1975462     1  0.3122     0.2765 0.816 0.000 0.160 0.020 0.000 NA
#&gt; SRR1975459     2  0.0405     0.7873 0.000 0.988 0.000 0.008 0.000 NA
#&gt; SRR1975460     2  0.0405     0.7873 0.000 0.988 0.000 0.008 0.000 NA
#&gt; SRR1975457     1  0.4088     0.4788 0.792 0.004 0.020 0.048 0.128 NA
#&gt; SRR1975458     1  0.4088     0.4788 0.792 0.004 0.020 0.048 0.128 NA
#&gt; SRR1975455     1  0.5233     0.4173 0.676 0.004 0.032 0.044 0.228 NA
#&gt; SRR1975456     1  0.5233     0.4173 0.676 0.004 0.032 0.044 0.228 NA
#&gt; SRR1975453     1  0.3854     0.4853 0.824 0.000 0.028 0.080 0.040 NA
#&gt; SRR1975454     1  0.3854     0.4853 0.824 0.000 0.028 0.080 0.040 NA
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-5-a').click(function(){
  $('#tab-CV-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-kmeans-signature_compare](figure_cola/CV-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-kmeans-collect-classes](figure_cola/CV-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:skmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "skmeans"]
# you can also extract it by
# res = res_list["CV:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-skmeans-collect-plots](figure_cola/CV-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-skmeans-select-partition-number](figure_cola/CV-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.805           0.911       0.957         0.4654 0.556   0.556
#> 3 3 0.678           0.879       0.937         0.4107 0.771   0.589
#> 4 4 0.704           0.634       0.848         0.1393 0.836   0.566
#> 5 5 0.720           0.762       0.838         0.0657 0.852   0.517
#> 6 6 0.751           0.660       0.775         0.0438 0.935   0.699
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-classes'>
<ul>
<li><a href='#tab-CV-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-skmeans-get-classes-1'>
<p><a id='tab-CV-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975507     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975506     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975505     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975503     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975504     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975501     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975502     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975499     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975500     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975497     1  0.0672      0.931 0.992 0.008
#&gt; SRR1975498     1  0.0672      0.931 0.992 0.008
#&gt; SRR1975493     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975494     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975495     1  0.0938      0.931 0.988 0.012
#&gt; SRR1975496     1  0.0938      0.931 0.988 0.012
#&gt; SRR1975491     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975492     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975489     1  0.0672      0.931 0.992 0.008
#&gt; SRR1975490     1  0.0672      0.931 0.992 0.008
#&gt; SRR1975487     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975488     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975485     1  0.0672      0.931 0.992 0.008
#&gt; SRR1975486     1  0.0672      0.931 0.992 0.008
#&gt; SRR1975483     1  0.2236      0.919 0.964 0.036
#&gt; SRR1975484     1  0.2236      0.919 0.964 0.036
#&gt; SRR1975481     1  0.2236      0.919 0.964 0.036
#&gt; SRR1975482     1  0.2236      0.919 0.964 0.036
#&gt; SRR1975477     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975478     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975479     1  0.3431      0.898 0.936 0.064
#&gt; SRR1975480     1  0.3431      0.898 0.936 0.064
#&gt; SRR1975475     1  0.0938      0.931 0.988 0.012
#&gt; SRR1975476     1  0.0938      0.931 0.988 0.012
#&gt; SRR1975473     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975474     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975471     2  0.0376      0.996 0.004 0.996
#&gt; SRR1975472     2  0.0376      0.996 0.004 0.996
#&gt; SRR1975469     1  0.1184      0.929 0.984 0.016
#&gt; SRR1975470     1  0.1184      0.929 0.984 0.016
#&gt; SRR1975467     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975468     1  0.0000      0.931 1.000 0.000
#&gt; SRR1975465     1  0.9209      0.560 0.664 0.336
#&gt; SRR1975466     1  0.9209      0.560 0.664 0.336
#&gt; SRR1975463     1  0.9209      0.560 0.664 0.336
#&gt; SRR1975464     1  0.9209      0.560 0.664 0.336
#&gt; SRR1975461     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975462     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975459     1  0.9209      0.560 0.664 0.336
#&gt; SRR1975460     1  0.9209      0.560 0.664 0.336
#&gt; SRR1975457     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975458     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975455     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975456     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975453     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975454     2  0.0000      0.999 0.000 1.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-1-a').click(function(){
  $('#tab-CV-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-2'>
<p><a id='tab-CV-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3   0.000      0.922 0.000 0.000 1.000
#&gt; SRR1975507     3   0.000      0.922 0.000 0.000 1.000
#&gt; SRR1975506     3   0.000      0.922 0.000 0.000 1.000
#&gt; SRR1975505     3   0.000      0.922 0.000 0.000 1.000
#&gt; SRR1975503     2   0.435      0.782 0.184 0.816 0.000
#&gt; SRR1975504     2   0.435      0.782 0.184 0.816 0.000
#&gt; SRR1975501     2   0.579      0.622 0.332 0.668 0.000
#&gt; SRR1975502     2   0.579      0.622 0.332 0.668 0.000
#&gt; SRR1975499     1   0.429      0.752 0.820 0.180 0.000
#&gt; SRR1975500     1   0.429      0.752 0.820 0.180 0.000
#&gt; SRR1975497     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975498     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975493     2   0.000      0.872 0.000 1.000 0.000
#&gt; SRR1975494     2   0.000      0.872 0.000 1.000 0.000
#&gt; SRR1975495     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975496     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975491     2   0.579      0.622 0.332 0.668 0.000
#&gt; SRR1975492     2   0.579      0.622 0.332 0.668 0.000
#&gt; SRR1975489     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975490     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975487     1   0.355      0.823 0.868 0.132 0.000
#&gt; SRR1975488     1   0.355      0.823 0.868 0.132 0.000
#&gt; SRR1975485     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975486     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975483     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975484     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975481     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975482     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975477     3   0.418      0.847 0.172 0.000 0.828
#&gt; SRR1975478     3   0.418      0.847 0.172 0.000 0.828
#&gt; SRR1975479     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975480     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975475     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975476     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975473     3   0.435      0.839 0.184 0.000 0.816
#&gt; SRR1975474     3   0.435      0.839 0.184 0.000 0.816
#&gt; SRR1975471     3   0.510      0.768 0.248 0.000 0.752
#&gt; SRR1975472     3   0.510      0.768 0.248 0.000 0.752
#&gt; SRR1975469     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975470     1   0.000      0.962 1.000 0.000 0.000
#&gt; SRR1975467     2   0.000      0.872 0.000 1.000 0.000
#&gt; SRR1975468     2   0.000      0.872 0.000 1.000 0.000
#&gt; SRR1975465     2   0.000      0.872 0.000 1.000 0.000
#&gt; SRR1975466     2   0.000      0.872 0.000 1.000 0.000
#&gt; SRR1975463     2   0.000      0.872 0.000 1.000 0.000
#&gt; SRR1975464     2   0.000      0.872 0.000 1.000 0.000
#&gt; SRR1975461     3   0.000      0.922 0.000 0.000 1.000
#&gt; SRR1975462     3   0.000      0.922 0.000 0.000 1.000
#&gt; SRR1975459     2   0.000      0.872 0.000 1.000 0.000
#&gt; SRR1975460     2   0.000      0.872 0.000 1.000 0.000
#&gt; SRR1975457     3   0.000      0.922 0.000 0.000 1.000
#&gt; SRR1975458     3   0.000      0.922 0.000 0.000 1.000
#&gt; SRR1975455     3   0.000      0.922 0.000 0.000 1.000
#&gt; SRR1975456     3   0.000      0.922 0.000 0.000 1.000
#&gt; SRR1975453     3   0.000      0.922 0.000 0.000 1.000
#&gt; SRR1975454     3   0.000      0.922 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-2-a').click(function(){
  $('#tab-CV-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-3'>
<p><a id='tab-CV-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.0000    0.84848 0.000 0.000 1.000 0.000
#&gt; SRR1975507     3  0.0000    0.84848 0.000 0.000 1.000 0.000
#&gt; SRR1975506     3  0.0000    0.84848 0.000 0.000 1.000 0.000
#&gt; SRR1975505     3  0.0000    0.84848 0.000 0.000 1.000 0.000
#&gt; SRR1975503     4  0.4992    0.02340 0.000 0.476 0.000 0.524
#&gt; SRR1975504     4  0.4992    0.02340 0.000 0.476 0.000 0.524
#&gt; SRR1975501     2  0.5850    0.01172 0.032 0.512 0.000 0.456
#&gt; SRR1975502     2  0.5850    0.01172 0.032 0.512 0.000 0.456
#&gt; SRR1975499     4  0.0779    0.69260 0.004 0.016 0.000 0.980
#&gt; SRR1975500     4  0.0779    0.69260 0.004 0.016 0.000 0.980
#&gt; SRR1975497     4  0.4356    0.36906 0.292 0.000 0.000 0.708
#&gt; SRR1975498     4  0.4356    0.36906 0.292 0.000 0.000 0.708
#&gt; SRR1975493     2  0.0000    0.89276 0.000 1.000 0.000 0.000
#&gt; SRR1975494     2  0.0000    0.89276 0.000 1.000 0.000 0.000
#&gt; SRR1975495     1  0.4454    0.63504 0.692 0.000 0.000 0.308
#&gt; SRR1975496     1  0.4454    0.63504 0.692 0.000 0.000 0.308
#&gt; SRR1975491     4  0.5165   -0.00674 0.004 0.484 0.000 0.512
#&gt; SRR1975492     4  0.5165   -0.00674 0.004 0.484 0.000 0.512
#&gt; SRR1975489     4  0.1022    0.68976 0.032 0.000 0.000 0.968
#&gt; SRR1975490     4  0.1022    0.68976 0.032 0.000 0.000 0.968
#&gt; SRR1975487     4  0.0188    0.69383 0.004 0.000 0.000 0.996
#&gt; SRR1975488     4  0.0188    0.69383 0.004 0.000 0.000 0.996
#&gt; SRR1975485     4  0.0592    0.69227 0.016 0.000 0.000 0.984
#&gt; SRR1975486     4  0.0592    0.69227 0.016 0.000 0.000 0.984
#&gt; SRR1975483     1  0.2973    0.83565 0.856 0.000 0.000 0.144
#&gt; SRR1975484     1  0.2973    0.83565 0.856 0.000 0.000 0.144
#&gt; SRR1975481     1  0.2530    0.83323 0.888 0.000 0.000 0.112
#&gt; SRR1975482     1  0.2530    0.83323 0.888 0.000 0.000 0.112
#&gt; SRR1975477     3  0.5070    0.47277 0.416 0.000 0.580 0.004
#&gt; SRR1975478     3  0.5070    0.47277 0.416 0.000 0.580 0.004
#&gt; SRR1975479     4  0.4804    0.29923 0.384 0.000 0.000 0.616
#&gt; SRR1975480     4  0.4804    0.29923 0.384 0.000 0.000 0.616
#&gt; SRR1975475     4  0.0921    0.69162 0.028 0.000 0.000 0.972
#&gt; SRR1975476     4  0.0921    0.69162 0.028 0.000 0.000 0.972
#&gt; SRR1975473     3  0.5500    0.37031 0.464 0.000 0.520 0.016
#&gt; SRR1975474     3  0.5500    0.37031 0.464 0.000 0.520 0.016
#&gt; SRR1975471     1  0.0657    0.79585 0.984 0.000 0.012 0.004
#&gt; SRR1975472     1  0.0657    0.79585 0.984 0.000 0.012 0.004
#&gt; SRR1975469     4  0.4746    0.18014 0.368 0.000 0.000 0.632
#&gt; SRR1975470     4  0.4746    0.18014 0.368 0.000 0.000 0.632
#&gt; SRR1975467     2  0.0000    0.89276 0.000 1.000 0.000 0.000
#&gt; SRR1975468     2  0.0000    0.89276 0.000 1.000 0.000 0.000
#&gt; SRR1975465     2  0.0000    0.89276 0.000 1.000 0.000 0.000
#&gt; SRR1975466     2  0.0000    0.89276 0.000 1.000 0.000 0.000
#&gt; SRR1975463     2  0.0000    0.89276 0.000 1.000 0.000 0.000
#&gt; SRR1975464     2  0.0000    0.89276 0.000 1.000 0.000 0.000
#&gt; SRR1975461     3  0.1118    0.83618 0.036 0.000 0.964 0.000
#&gt; SRR1975462     3  0.1118    0.83618 0.036 0.000 0.964 0.000
#&gt; SRR1975459     2  0.0000    0.89276 0.000 1.000 0.000 0.000
#&gt; SRR1975460     2  0.0000    0.89276 0.000 1.000 0.000 0.000
#&gt; SRR1975457     3  0.0000    0.84848 0.000 0.000 1.000 0.000
#&gt; SRR1975458     3  0.0000    0.84848 0.000 0.000 1.000 0.000
#&gt; SRR1975455     3  0.0188    0.84752 0.004 0.000 0.996 0.000
#&gt; SRR1975456     3  0.0188    0.84752 0.004 0.000 0.996 0.000
#&gt; SRR1975453     3  0.2704    0.77747 0.124 0.000 0.876 0.000
#&gt; SRR1975454     3  0.2704    0.77747 0.124 0.000 0.876 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-3-a').click(function(){
  $('#tab-CV-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-4'>
<p><a id='tab-CV-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.0162      0.934 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975507     3  0.0162      0.934 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975506     3  0.0162      0.934 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975505     3  0.0162      0.934 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975503     4  0.3968      0.648 0.004 0.204 0.000 0.768 0.024
#&gt; SRR1975504     4  0.3968      0.648 0.004 0.204 0.000 0.768 0.024
#&gt; SRR1975501     4  0.6546      0.454 0.096 0.328 0.000 0.536 0.040
#&gt; SRR1975502     4  0.6546      0.454 0.096 0.328 0.000 0.536 0.040
#&gt; SRR1975499     4  0.0451      0.711 0.008 0.000 0.000 0.988 0.004
#&gt; SRR1975500     4  0.0451      0.711 0.008 0.000 0.000 0.988 0.004
#&gt; SRR1975497     1  0.5080      0.403 0.604 0.000 0.000 0.348 0.048
#&gt; SRR1975498     1  0.5080      0.403 0.604 0.000 0.000 0.348 0.048
#&gt; SRR1975493     2  0.0162      0.992 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1975494     2  0.0162      0.992 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1975495     1  0.2376      0.720 0.904 0.000 0.000 0.052 0.044
#&gt; SRR1975496     1  0.2376      0.720 0.904 0.000 0.000 0.052 0.044
#&gt; SRR1975491     4  0.5677      0.557 0.044 0.284 0.000 0.632 0.040
#&gt; SRR1975492     4  0.5677      0.557 0.044 0.284 0.000 0.632 0.040
#&gt; SRR1975489     4  0.4657      0.634 0.108 0.000 0.000 0.740 0.152
#&gt; SRR1975490     4  0.4657      0.634 0.108 0.000 0.000 0.740 0.152
#&gt; SRR1975487     4  0.0693      0.711 0.012 0.000 0.000 0.980 0.008
#&gt; SRR1975488     4  0.0693      0.711 0.012 0.000 0.000 0.980 0.008
#&gt; SRR1975485     4  0.3861      0.658 0.128 0.000 0.000 0.804 0.068
#&gt; SRR1975486     4  0.3861      0.658 0.128 0.000 0.000 0.804 0.068
#&gt; SRR1975483     1  0.2236      0.738 0.908 0.000 0.000 0.024 0.068
#&gt; SRR1975484     1  0.2236      0.738 0.908 0.000 0.000 0.024 0.068
#&gt; SRR1975481     1  0.2966      0.713 0.848 0.000 0.000 0.016 0.136
#&gt; SRR1975482     1  0.2966      0.713 0.848 0.000 0.000 0.016 0.136
#&gt; SRR1975477     5  0.3160      0.793 0.004 0.000 0.188 0.000 0.808
#&gt; SRR1975478     5  0.3160      0.793 0.004 0.000 0.188 0.000 0.808
#&gt; SRR1975479     5  0.4431      0.585 0.052 0.000 0.000 0.216 0.732
#&gt; SRR1975480     5  0.4431      0.585 0.052 0.000 0.000 0.216 0.732
#&gt; SRR1975475     4  0.5163      0.605 0.152 0.000 0.000 0.692 0.156
#&gt; SRR1975476     4  0.5163      0.605 0.152 0.000 0.000 0.692 0.156
#&gt; SRR1975473     5  0.2843      0.806 0.008 0.000 0.144 0.000 0.848
#&gt; SRR1975474     5  0.2843      0.806 0.008 0.000 0.144 0.000 0.848
#&gt; SRR1975471     1  0.3807      0.636 0.748 0.000 0.012 0.000 0.240
#&gt; SRR1975472     1  0.3807      0.636 0.748 0.000 0.012 0.000 0.240
#&gt; SRR1975469     1  0.5272      0.544 0.620 0.000 0.000 0.308 0.072
#&gt; SRR1975470     1  0.5272      0.544 0.620 0.000 0.000 0.308 0.072
#&gt; SRR1975467     2  0.0798      0.978 0.000 0.976 0.000 0.008 0.016
#&gt; SRR1975468     2  0.0798      0.978 0.000 0.976 0.000 0.008 0.016
#&gt; SRR1975465     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975461     3  0.1809      0.909 0.012 0.000 0.928 0.000 0.060
#&gt; SRR1975462     3  0.1809      0.909 0.012 0.000 0.928 0.000 0.060
#&gt; SRR1975459     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975457     3  0.1410      0.915 0.000 0.000 0.940 0.000 0.060
#&gt; SRR1975458     3  0.1410      0.915 0.000 0.000 0.940 0.000 0.060
#&gt; SRR1975455     3  0.1908      0.894 0.000 0.000 0.908 0.000 0.092
#&gt; SRR1975456     3  0.1908      0.894 0.000 0.000 0.908 0.000 0.092
#&gt; SRR1975453     3  0.2359      0.893 0.036 0.000 0.904 0.000 0.060
#&gt; SRR1975454     3  0.2359      0.893 0.036 0.000 0.904 0.000 0.060
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-4-a').click(function(){
  $('#tab-CV-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-5'>
<p><a id='tab-CV-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     3  0.0363     0.8778 0.000 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1975507     3  0.0363     0.8778 0.000 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1975506     3  0.0363     0.8778 0.000 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1975505     3  0.0363     0.8778 0.000 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1975503     6  0.5029     0.5004 0.000 0.092 0.000 0.328 0.000 0.580
#&gt; SRR1975504     6  0.5029     0.5004 0.000 0.092 0.000 0.328 0.000 0.580
#&gt; SRR1975501     6  0.5690     0.6875 0.040 0.212 0.000 0.104 0.008 0.636
#&gt; SRR1975502     6  0.5690     0.6875 0.040 0.212 0.000 0.104 0.008 0.636
#&gt; SRR1975499     4  0.3860     0.0338 0.000 0.000 0.000 0.528 0.000 0.472
#&gt; SRR1975500     4  0.3860     0.0338 0.000 0.000 0.000 0.528 0.000 0.472
#&gt; SRR1975497     4  0.5901    -0.0575 0.304 0.000 0.000 0.464 0.000 0.232
#&gt; SRR1975498     4  0.5901    -0.0575 0.304 0.000 0.000 0.464 0.000 0.232
#&gt; SRR1975493     2  0.1007     0.9445 0.000 0.956 0.000 0.000 0.000 0.044
#&gt; SRR1975494     2  0.1007     0.9445 0.000 0.956 0.000 0.000 0.000 0.044
#&gt; SRR1975495     1  0.5400     0.5386 0.624 0.000 0.000 0.180 0.012 0.184
#&gt; SRR1975496     1  0.5400     0.5386 0.624 0.000 0.000 0.180 0.012 0.184
#&gt; SRR1975491     6  0.4894     0.7346 0.012 0.152 0.000 0.120 0.008 0.708
#&gt; SRR1975492     6  0.4894     0.7346 0.012 0.152 0.000 0.120 0.008 0.708
#&gt; SRR1975489     4  0.4236     0.5116 0.044 0.000 0.000 0.780 0.088 0.088
#&gt; SRR1975490     4  0.4236     0.5116 0.044 0.000 0.000 0.780 0.088 0.088
#&gt; SRR1975487     4  0.3765     0.2142 0.000 0.000 0.000 0.596 0.000 0.404
#&gt; SRR1975488     4  0.3765     0.2142 0.000 0.000 0.000 0.596 0.000 0.404
#&gt; SRR1975485     4  0.1769     0.5506 0.012 0.000 0.000 0.924 0.004 0.060
#&gt; SRR1975486     4  0.1769     0.5506 0.012 0.000 0.000 0.924 0.004 0.060
#&gt; SRR1975483     1  0.1857     0.7293 0.928 0.000 0.000 0.032 0.028 0.012
#&gt; SRR1975484     1  0.1857     0.7293 0.928 0.000 0.000 0.032 0.028 0.012
#&gt; SRR1975481     1  0.2583     0.7245 0.884 0.000 0.000 0.052 0.056 0.008
#&gt; SRR1975482     1  0.2583     0.7245 0.884 0.000 0.000 0.052 0.056 0.008
#&gt; SRR1975477     5  0.2703     0.7850 0.016 0.000 0.116 0.000 0.860 0.008
#&gt; SRR1975478     5  0.2703     0.7850 0.016 0.000 0.116 0.000 0.860 0.008
#&gt; SRR1975479     5  0.4761     0.5042 0.024 0.000 0.000 0.352 0.600 0.024
#&gt; SRR1975480     5  0.4761     0.5042 0.024 0.000 0.000 0.352 0.600 0.024
#&gt; SRR1975475     4  0.2886     0.5212 0.028 0.000 0.000 0.872 0.040 0.060
#&gt; SRR1975476     4  0.2886     0.5212 0.028 0.000 0.000 0.872 0.040 0.060
#&gt; SRR1975473     5  0.2095     0.7931 0.016 0.000 0.076 0.004 0.904 0.000
#&gt; SRR1975474     5  0.2095     0.7931 0.016 0.000 0.076 0.004 0.904 0.000
#&gt; SRR1975471     1  0.3686     0.6519 0.788 0.000 0.000 0.000 0.124 0.088
#&gt; SRR1975472     1  0.3686     0.6519 0.788 0.000 0.000 0.000 0.124 0.088
#&gt; SRR1975469     1  0.5291     0.2820 0.492 0.000 0.000 0.428 0.012 0.068
#&gt; SRR1975470     1  0.5291     0.2820 0.492 0.000 0.000 0.428 0.012 0.068
#&gt; SRR1975467     2  0.1908     0.8947 0.000 0.900 0.000 0.000 0.004 0.096
#&gt; SRR1975468     2  0.1908     0.8947 0.000 0.900 0.000 0.000 0.004 0.096
#&gt; SRR1975465     2  0.0000     0.9640 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000     0.9640 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0000     0.9640 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975464     2  0.0000     0.9640 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975461     3  0.3408     0.8320 0.016 0.000 0.832 0.000 0.072 0.080
#&gt; SRR1975462     3  0.3408     0.8320 0.016 0.000 0.832 0.000 0.072 0.080
#&gt; SRR1975459     2  0.0000     0.9640 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000     0.9640 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975457     3  0.2563     0.8547 0.004 0.000 0.880 0.000 0.076 0.040
#&gt; SRR1975458     3  0.2563     0.8547 0.004 0.000 0.880 0.000 0.076 0.040
#&gt; SRR1975455     3  0.2932     0.8072 0.004 0.000 0.836 0.000 0.140 0.020
#&gt; SRR1975456     3  0.2932     0.8072 0.004 0.000 0.836 0.000 0.140 0.020
#&gt; SRR1975453     3  0.4220     0.8039 0.056 0.000 0.784 0.000 0.076 0.084
#&gt; SRR1975454     3  0.4220     0.8039 0.056 0.000 0.784 0.000 0.076 0.084
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-5-a').click(function(){
  $('#tab-CV-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-skmeans-signature_compare](figure_cola/CV-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-skmeans-collect-classes](figure_cola/CV-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "pam"]
# you can also extract it by
# res = res_list["CV:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-pam-collect-plots](figure_cola/CV-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-pam-select-partition-number](figure_cola/CV-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.992           0.981       0.990         0.2078 0.805   0.805
#> 3 3 0.590           0.910       0.935         1.0078 0.782   0.729
#> 4 4 0.865           0.925       0.971         0.4110 0.808   0.678
#> 5 5 0.971           0.937       0.975         0.1208 0.906   0.778
#> 6 6 0.950           0.932       0.947         0.0336 0.984   0.953
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-classes'>
<ul>
<li><a href='#tab-CV-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-pam-get-classes-1'>
<p><a id='tab-CV-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.0000      0.995 0.000 1.000
#&gt; SRR1975507     2  0.0000      0.995 0.000 1.000
#&gt; SRR1975506     2  0.0000      0.995 0.000 1.000
#&gt; SRR1975505     2  0.0000      0.995 0.000 1.000
#&gt; SRR1975503     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975504     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975501     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975502     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975499     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975500     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975497     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975498     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975493     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975494     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975495     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975496     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975491     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975492     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975489     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975490     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975487     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975488     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975485     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975486     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975483     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975484     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975481     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975482     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975477     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975478     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975479     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975480     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975475     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975476     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975473     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975474     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975471     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975472     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975469     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975470     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975467     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975468     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975465     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975466     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975463     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975464     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975461     2  0.0938      0.990 0.012 0.988
#&gt; SRR1975462     2  0.0938      0.990 0.012 0.988
#&gt; SRR1975459     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975460     1  0.0000      0.989 1.000 0.000
#&gt; SRR1975457     1  0.4298      0.913 0.912 0.088
#&gt; SRR1975458     1  0.4298      0.913 0.912 0.088
#&gt; SRR1975455     1  0.4298      0.913 0.912 0.088
#&gt; SRR1975456     1  0.4298      0.913 0.912 0.088
#&gt; SRR1975453     1  0.4298      0.913 0.912 0.088
#&gt; SRR1975454     1  0.4298      0.913 0.912 0.088
</code></pre>

<script>
$('#tab-CV-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-1-a').click(function(){
  $('#tab-CV-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-2'>
<p><a id='tab-CV-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.0000      0.910 0.000 0.000 1.000
#&gt; SRR1975507     3  0.0000      0.910 0.000 0.000 1.000
#&gt; SRR1975506     3  0.0000      0.910 0.000 0.000 1.000
#&gt; SRR1975505     3  0.0000      0.910 0.000 0.000 1.000
#&gt; SRR1975503     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975504     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975501     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975502     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975499     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975500     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975497     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975493     2  0.4974      0.881 0.236 0.764 0.000
#&gt; SRR1975494     2  0.5016      0.875 0.240 0.760 0.000
#&gt; SRR1975495     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975491     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975492     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975489     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975490     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975487     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975488     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975485     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975486     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975483     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975477     1  0.0747      0.936 0.984 0.016 0.000
#&gt; SRR1975478     1  0.0747      0.936 0.984 0.016 0.000
#&gt; SRR1975479     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975480     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975475     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975476     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975473     1  0.0237      0.944 0.996 0.004 0.000
#&gt; SRR1975474     1  0.0237      0.944 0.996 0.004 0.000
#&gt; SRR1975471     1  0.3941      0.819 0.844 0.156 0.000
#&gt; SRR1975472     1  0.3941      0.819 0.844 0.156 0.000
#&gt; SRR1975469     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975470     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1975467     1  0.3192      0.822 0.888 0.112 0.000
#&gt; SRR1975468     1  0.3192      0.822 0.888 0.112 0.000
#&gt; SRR1975465     2  0.4002      0.959 0.160 0.840 0.000
#&gt; SRR1975466     2  0.4002      0.959 0.160 0.840 0.000
#&gt; SRR1975463     2  0.4002      0.959 0.160 0.840 0.000
#&gt; SRR1975464     2  0.4002      0.959 0.160 0.840 0.000
#&gt; SRR1975461     3  0.5777      0.813 0.052 0.160 0.788
#&gt; SRR1975462     3  0.5777      0.813 0.052 0.160 0.788
#&gt; SRR1975459     2  0.4002      0.959 0.160 0.840 0.000
#&gt; SRR1975460     2  0.4002      0.959 0.160 0.840 0.000
#&gt; SRR1975457     1  0.5573      0.777 0.796 0.160 0.044
#&gt; SRR1975458     1  0.5573      0.777 0.796 0.160 0.044
#&gt; SRR1975455     1  0.5573      0.777 0.796 0.160 0.044
#&gt; SRR1975456     1  0.5573      0.777 0.796 0.160 0.044
#&gt; SRR1975453     1  0.5573      0.777 0.796 0.160 0.044
#&gt; SRR1975454     1  0.5573      0.777 0.796 0.160 0.044
</code></pre>

<script>
$('#tab-CV-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-2-a').click(function(){
  $('#tab-CV-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-3'>
<p><a id='tab-CV-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1975503     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975504     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975501     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975502     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975499     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975500     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975497     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975498     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975493     2  0.2868      0.772 0.000 0.864  0 0.136
#&gt; SRR1975494     2  0.2973      0.760 0.000 0.856  0 0.144
#&gt; SRR1975495     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975496     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975491     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975492     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975489     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975490     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975487     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975488     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975485     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975486     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975483     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975484     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975481     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975482     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975477     4  0.4406      0.581 0.300 0.000  0 0.700
#&gt; SRR1975478     4  0.4454      0.565 0.308 0.000  0 0.692
#&gt; SRR1975479     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975480     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975475     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975476     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975473     4  0.1716      0.913 0.064 0.000  0 0.936
#&gt; SRR1975474     4  0.1716      0.913 0.064 0.000  0 0.936
#&gt; SRR1975471     1  0.3219      0.749 0.836 0.000  0 0.164
#&gt; SRR1975472     1  0.3172      0.756 0.840 0.000  0 0.160
#&gt; SRR1975469     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975470     4  0.0000      0.968 0.000 0.000  0 1.000
#&gt; SRR1975467     4  0.2760      0.840 0.000 0.128  0 0.872
#&gt; SRR1975468     4  0.2760      0.840 0.000 0.128  0 0.872
#&gt; SRR1975465     2  0.0000      0.924 0.000 1.000  0 0.000
#&gt; SRR1975466     2  0.0000      0.924 0.000 1.000  0 0.000
#&gt; SRR1975463     2  0.0000      0.924 0.000 1.000  0 0.000
#&gt; SRR1975464     2  0.0000      0.924 0.000 1.000  0 0.000
#&gt; SRR1975461     1  0.0000      0.935 1.000 0.000  0 0.000
#&gt; SRR1975462     1  0.0000      0.935 1.000 0.000  0 0.000
#&gt; SRR1975459     2  0.0000      0.924 0.000 1.000  0 0.000
#&gt; SRR1975460     2  0.0000      0.924 0.000 1.000  0 0.000
#&gt; SRR1975457     1  0.0000      0.935 1.000 0.000  0 0.000
#&gt; SRR1975458     1  0.0000      0.935 1.000 0.000  0 0.000
#&gt; SRR1975455     1  0.0469      0.929 0.988 0.000  0 0.012
#&gt; SRR1975456     1  0.0469      0.929 0.988 0.000  0 0.012
#&gt; SRR1975453     1  0.0000      0.935 1.000 0.000  0 0.000
#&gt; SRR1975454     1  0.0000      0.935 1.000 0.000  0 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-3-a').click(function(){
  $('#tab-CV-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-4'>
<p><a id='tab-CV-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5
#&gt; SRR1975508     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975507     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975506     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975505     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975503     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975504     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975501     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975502     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975499     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975500     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975497     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975498     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975493     2   0.314      0.676 0.000 0.796  0 0.204 0.000
#&gt; SRR1975494     2   0.318      0.670 0.000 0.792  0 0.208 0.000
#&gt; SRR1975495     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975496     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975491     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975492     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975489     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975490     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975487     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975488     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975485     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975486     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975483     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975484     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975481     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975482     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975477     5   0.000      0.859 0.000 0.000  0 0.000 1.000
#&gt; SRR1975478     5   0.000      0.859 0.000 0.000  0 0.000 1.000
#&gt; SRR1975479     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975480     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975475     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975476     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975473     5   0.000      0.859 0.000 0.000  0 0.000 1.000
#&gt; SRR1975474     5   0.000      0.859 0.000 0.000  0 0.000 1.000
#&gt; SRR1975471     1   0.134      0.889 0.944 0.000  0 0.056 0.000
#&gt; SRR1975472     1   0.134      0.889 0.944 0.000  0 0.056 0.000
#&gt; SRR1975469     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975470     4   0.000      0.995 0.000 0.000  0 1.000 0.000
#&gt; SRR1975467     4   0.148      0.930 0.000 0.064  0 0.936 0.000
#&gt; SRR1975468     4   0.148      0.930 0.000 0.064  0 0.936 0.000
#&gt; SRR1975465     2   0.000      0.892 0.000 1.000  0 0.000 0.000
#&gt; SRR1975466     2   0.000      0.892 0.000 1.000  0 0.000 0.000
#&gt; SRR1975463     2   0.000      0.892 0.000 1.000  0 0.000 0.000
#&gt; SRR1975464     2   0.000      0.892 0.000 1.000  0 0.000 0.000
#&gt; SRR1975461     1   0.000      0.938 1.000 0.000  0 0.000 0.000
#&gt; SRR1975462     1   0.000      0.938 1.000 0.000  0 0.000 0.000
#&gt; SRR1975459     2   0.000      0.892 0.000 1.000  0 0.000 0.000
#&gt; SRR1975460     2   0.000      0.892 0.000 1.000  0 0.000 0.000
#&gt; SRR1975457     1   0.185      0.885 0.912 0.000  0 0.000 0.088
#&gt; SRR1975458     1   0.185      0.885 0.912 0.000  0 0.000 0.088
#&gt; SRR1975455     5   0.388      0.662 0.288 0.000  0 0.004 0.708
#&gt; SRR1975456     5   0.388      0.662 0.288 0.000  0 0.004 0.708
#&gt; SRR1975453     1   0.000      0.938 1.000 0.000  0 0.000 0.000
#&gt; SRR1975454     1   0.000      0.938 1.000 0.000  0 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-4-a').click(function(){
  $('#tab-CV-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-5'>
<p><a id='tab-CV-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5    p6
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975503     4  0.0000      0.960 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975504     4  0.0000      0.960 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975501     4  0.0000      0.960 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975502     4  0.0000      0.960 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975499     4  0.0000      0.960 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975500     4  0.0000      0.960 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975497     4  0.1625      0.953 0.060 0.000  0 0.928 0.000 0.012
#&gt; SRR1975498     4  0.1625      0.953 0.060 0.000  0 0.928 0.000 0.012
#&gt; SRR1975493     2  0.3582      0.696 0.000 0.768  0 0.196 0.000 0.036
#&gt; SRR1975494     2  0.3612      0.690 0.000 0.764  0 0.200 0.000 0.036
#&gt; SRR1975495     4  0.1563      0.954 0.056 0.000  0 0.932 0.000 0.012
#&gt; SRR1975496     4  0.1563      0.954 0.056 0.000  0 0.932 0.000 0.012
#&gt; SRR1975491     4  0.0000      0.960 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975492     4  0.0000      0.960 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975489     4  0.0146      0.961 0.000 0.000  0 0.996 0.000 0.004
#&gt; SRR1975490     4  0.0291      0.961 0.004 0.000  0 0.992 0.000 0.004
#&gt; SRR1975487     4  0.0000      0.960 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975488     4  0.0000      0.960 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975485     4  0.0891      0.960 0.024 0.000  0 0.968 0.000 0.008
#&gt; SRR1975486     4  0.1074      0.959 0.028 0.000  0 0.960 0.000 0.012
#&gt; SRR1975483     4  0.1967      0.941 0.084 0.000  0 0.904 0.000 0.012
#&gt; SRR1975484     4  0.1967      0.941 0.084 0.000  0 0.904 0.000 0.012
#&gt; SRR1975481     4  0.1967      0.941 0.084 0.000  0 0.904 0.000 0.012
#&gt; SRR1975482     4  0.1967      0.941 0.084 0.000  0 0.904 0.000 0.012
#&gt; SRR1975477     5  0.0000      0.957 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975478     5  0.0000      0.957 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975479     4  0.1745      0.950 0.068 0.000  0 0.920 0.000 0.012
#&gt; SRR1975480     4  0.1745      0.950 0.068 0.000  0 0.920 0.000 0.012
#&gt; SRR1975475     4  0.0260      0.961 0.008 0.000  0 0.992 0.000 0.000
#&gt; SRR1975476     4  0.0260      0.961 0.008 0.000  0 0.992 0.000 0.000
#&gt; SRR1975473     5  0.1421      0.957 0.028 0.000  0 0.000 0.944 0.028
#&gt; SRR1975474     5  0.1421      0.957 0.028 0.000  0 0.000 0.944 0.028
#&gt; SRR1975471     1  0.1297      0.812 0.948 0.000  0 0.040 0.000 0.012
#&gt; SRR1975472     1  0.1297      0.812 0.948 0.000  0 0.040 0.000 0.012
#&gt; SRR1975469     4  0.1745      0.950 0.068 0.000  0 0.920 0.000 0.012
#&gt; SRR1975470     4  0.1745      0.950 0.068 0.000  0 0.920 0.000 0.012
#&gt; SRR1975467     4  0.1204      0.922 0.000 0.056  0 0.944 0.000 0.000
#&gt; SRR1975468     4  0.1204      0.922 0.000 0.056  0 0.944 0.000 0.000
#&gt; SRR1975465     2  0.0000      0.902 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.902 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.902 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.902 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975461     1  0.1610      0.902 0.916 0.000  0 0.000 0.000 0.084
#&gt; SRR1975462     1  0.1610      0.902 0.916 0.000  0 0.000 0.000 0.084
#&gt; SRR1975459     2  0.0000      0.902 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.902 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975457     6  0.2219      0.937 0.136 0.000  0 0.000 0.000 0.864
#&gt; SRR1975458     6  0.2219      0.937 0.136 0.000  0 0.000 0.000 0.864
#&gt; SRR1975455     6  0.1204      0.940 0.056 0.000  0 0.000 0.000 0.944
#&gt; SRR1975456     6  0.1204      0.940 0.056 0.000  0 0.000 0.000 0.944
#&gt; SRR1975453     1  0.1610      0.902 0.916 0.000  0 0.000 0.000 0.084
#&gt; SRR1975454     1  0.1610      0.902 0.916 0.000  0 0.000 0.000 0.084
</code></pre>

<script>
$('#tab-CV-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-5-a').click(function(){
  $('#tab-CV-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-membership-heatmap'>
<ul>
<li><a href='#tab-CV-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-pam-signature_compare](figure_cola/CV-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-pam-dimension-reduction'>
<ul>
<li><a href='#tab-CV-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-pam-collect-classes](figure_cola/CV-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "mclust"]
# you can also extract it by
# res = res_list["CV:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-mclust-collect-plots](figure_cola/CV-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-mclust-select-partition-number](figure_cola/CV-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.384           0.811       0.859         0.4656 0.532   0.532
#> 3 3 0.562           0.715       0.840         0.3724 0.743   0.540
#> 4 4 0.565           0.722       0.788         0.1251 0.927   0.783
#> 5 5 0.639           0.712       0.725         0.0430 0.948   0.808
#> 6 6 0.744           0.691       0.835         0.0623 0.852   0.482
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-classes'>
<ul>
<li><a href='#tab-CV-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-mclust-get-classes-1'>
<p><a id='tab-CV-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.6247      0.677 0.156 0.844
#&gt; SRR1975507     2  0.6247      0.677 0.156 0.844
#&gt; SRR1975506     2  0.6247      0.677 0.156 0.844
#&gt; SRR1975505     2  0.6247      0.677 0.156 0.844
#&gt; SRR1975503     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975504     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975501     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975502     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975499     1  0.0672      0.988 0.992 0.008
#&gt; SRR1975500     1  0.0672      0.988 0.992 0.008
#&gt; SRR1975497     2  0.9754      0.635 0.408 0.592
#&gt; SRR1975498     2  0.9754      0.635 0.408 0.592
#&gt; SRR1975493     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975494     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975495     2  0.9661      0.658 0.392 0.608
#&gt; SRR1975496     2  0.9661      0.658 0.392 0.608
#&gt; SRR1975491     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975492     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975489     2  0.9209      0.701 0.336 0.664
#&gt; SRR1975490     2  0.9209      0.701 0.336 0.664
#&gt; SRR1975487     1  0.1633      0.969 0.976 0.024
#&gt; SRR1975488     1  0.1843      0.963 0.972 0.028
#&gt; SRR1975485     2  0.9635      0.661 0.388 0.612
#&gt; SRR1975486     2  0.9522      0.676 0.372 0.628
#&gt; SRR1975483     2  0.9686      0.653 0.396 0.604
#&gt; SRR1975484     2  0.9686      0.653 0.396 0.604
#&gt; SRR1975481     2  0.9087      0.707 0.324 0.676
#&gt; SRR1975482     2  0.9087      0.707 0.324 0.676
#&gt; SRR1975477     2  0.5059      0.772 0.112 0.888
#&gt; SRR1975478     2  0.5059      0.772 0.112 0.888
#&gt; SRR1975479     2  0.4431      0.771 0.092 0.908
#&gt; SRR1975480     2  0.4431      0.771 0.092 0.908
#&gt; SRR1975475     2  0.9209      0.701 0.336 0.664
#&gt; SRR1975476     2  0.9209      0.701 0.336 0.664
#&gt; SRR1975473     2  0.4690      0.771 0.100 0.900
#&gt; SRR1975474     2  0.4690      0.771 0.100 0.900
#&gt; SRR1975471     2  0.6712      0.726 0.176 0.824
#&gt; SRR1975472     2  0.6712      0.726 0.176 0.824
#&gt; SRR1975469     2  0.9635      0.662 0.388 0.612
#&gt; SRR1975470     2  0.9635      0.662 0.388 0.612
#&gt; SRR1975467     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975468     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975465     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975466     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975463     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975464     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975461     2  0.1184      0.746 0.016 0.984
#&gt; SRR1975462     2  0.1184      0.746 0.016 0.984
#&gt; SRR1975459     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975460     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975457     2  0.1184      0.746 0.016 0.984
#&gt; SRR1975458     2  0.1184      0.746 0.016 0.984
#&gt; SRR1975455     2  0.1184      0.746 0.016 0.984
#&gt; SRR1975456     2  0.1184      0.746 0.016 0.984
#&gt; SRR1975453     2  0.4022      0.759 0.080 0.920
#&gt; SRR1975454     2  0.4022      0.759 0.080 0.920
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-1-a').click(function(){
  $('#tab-CV-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-2'>
<p><a id='tab-CV-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.2261      0.809 0.068 0.000 0.932
#&gt; SRR1975507     3  0.2261      0.809 0.068 0.000 0.932
#&gt; SRR1975506     3  0.2261      0.809 0.068 0.000 0.932
#&gt; SRR1975505     3  0.2261      0.809 0.068 0.000 0.932
#&gt; SRR1975503     2  0.5058      0.770 0.244 0.756 0.000
#&gt; SRR1975504     2  0.5058      0.770 0.244 0.756 0.000
#&gt; SRR1975501     2  0.5016      0.772 0.240 0.760 0.000
#&gt; SRR1975502     2  0.5016      0.772 0.240 0.760 0.000
#&gt; SRR1975499     2  0.5760      0.664 0.328 0.672 0.000
#&gt; SRR1975500     2  0.5760      0.664 0.328 0.672 0.000
#&gt; SRR1975497     1  0.0000      0.809 1.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      0.809 1.000 0.000 0.000
#&gt; SRR1975493     2  0.1129      0.825 0.004 0.976 0.020
#&gt; SRR1975494     2  0.1129      0.825 0.004 0.976 0.020
#&gt; SRR1975495     1  0.0747      0.809 0.984 0.000 0.016
#&gt; SRR1975496     1  0.0747      0.809 0.984 0.000 0.016
#&gt; SRR1975491     2  0.5098      0.766 0.248 0.752 0.000
#&gt; SRR1975492     2  0.5098      0.766 0.248 0.752 0.000
#&gt; SRR1975489     1  0.2537      0.768 0.920 0.000 0.080
#&gt; SRR1975490     1  0.2537      0.768 0.920 0.000 0.080
#&gt; SRR1975487     1  0.6291     -0.217 0.532 0.468 0.000
#&gt; SRR1975488     1  0.6286     -0.205 0.536 0.464 0.000
#&gt; SRR1975485     1  0.0237      0.807 0.996 0.004 0.000
#&gt; SRR1975486     1  0.0237      0.807 0.996 0.004 0.000
#&gt; SRR1975483     1  0.0424      0.810 0.992 0.000 0.008
#&gt; SRR1975484     1  0.0424      0.810 0.992 0.000 0.008
#&gt; SRR1975481     1  0.0892      0.807 0.980 0.000 0.020
#&gt; SRR1975482     1  0.0892      0.807 0.980 0.000 0.020
#&gt; SRR1975477     3  0.5178      0.863 0.256 0.000 0.744
#&gt; SRR1975478     3  0.5178      0.863 0.256 0.000 0.744
#&gt; SRR1975479     3  0.5882      0.749 0.348 0.000 0.652
#&gt; SRR1975480     3  0.5882      0.749 0.348 0.000 0.652
#&gt; SRR1975475     1  0.2796      0.763 0.908 0.000 0.092
#&gt; SRR1975476     1  0.2796      0.763 0.908 0.000 0.092
#&gt; SRR1975473     3  0.5178      0.863 0.256 0.000 0.744
#&gt; SRR1975474     3  0.5178      0.863 0.256 0.000 0.744
#&gt; SRR1975471     1  0.4931      0.485 0.768 0.000 0.232
#&gt; SRR1975472     1  0.4931      0.485 0.768 0.000 0.232
#&gt; SRR1975469     1  0.0661      0.810 0.988 0.004 0.008
#&gt; SRR1975470     1  0.0661      0.810 0.988 0.004 0.008
#&gt; SRR1975467     2  0.0747      0.827 0.016 0.984 0.000
#&gt; SRR1975468     2  0.0747      0.827 0.016 0.984 0.000
#&gt; SRR1975465     2  0.2261      0.817 0.000 0.932 0.068
#&gt; SRR1975466     2  0.2261      0.817 0.000 0.932 0.068
#&gt; SRR1975463     2  0.2261      0.817 0.000 0.932 0.068
#&gt; SRR1975464     2  0.2261      0.817 0.000 0.932 0.068
#&gt; SRR1975461     3  0.5465      0.794 0.288 0.000 0.712
#&gt; SRR1975462     3  0.5465      0.794 0.288 0.000 0.712
#&gt; SRR1975459     2  0.4062      0.768 0.000 0.836 0.164
#&gt; SRR1975460     2  0.4062      0.768 0.000 0.836 0.164
#&gt; SRR1975457     3  0.4555      0.875 0.200 0.000 0.800
#&gt; SRR1975458     3  0.4555      0.875 0.200 0.000 0.800
#&gt; SRR1975455     3  0.4605      0.875 0.204 0.000 0.796
#&gt; SRR1975456     3  0.4605      0.875 0.204 0.000 0.796
#&gt; SRR1975453     1  0.6299     -0.308 0.524 0.000 0.476
#&gt; SRR1975454     1  0.6299     -0.308 0.524 0.000 0.476
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-2-a').click(function(){
  $('#tab-CV-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-3'>
<p><a id='tab-CV-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.0188      0.833 0.000 0.000 0.996 0.004
#&gt; SRR1975507     3  0.0188      0.833 0.000 0.000 0.996 0.004
#&gt; SRR1975506     3  0.0188      0.833 0.000 0.000 0.996 0.004
#&gt; SRR1975505     3  0.0188      0.833 0.000 0.000 0.996 0.004
#&gt; SRR1975503     2  0.3123      0.737 0.156 0.844 0.000 0.000
#&gt; SRR1975504     2  0.3123      0.737 0.156 0.844 0.000 0.000
#&gt; SRR1975501     2  0.3266      0.733 0.168 0.832 0.000 0.000
#&gt; SRR1975502     2  0.3266      0.733 0.168 0.832 0.000 0.000
#&gt; SRR1975499     2  0.3801      0.687 0.220 0.780 0.000 0.000
#&gt; SRR1975500     2  0.3837      0.682 0.224 0.776 0.000 0.000
#&gt; SRR1975497     1  0.2892      0.773 0.896 0.000 0.036 0.068
#&gt; SRR1975498     1  0.2816      0.775 0.900 0.000 0.036 0.064
#&gt; SRR1975493     2  0.1474      0.766 0.000 0.948 0.000 0.052
#&gt; SRR1975494     2  0.1474      0.766 0.000 0.948 0.000 0.052
#&gt; SRR1975495     1  0.0524      0.792 0.988 0.000 0.004 0.008
#&gt; SRR1975496     1  0.0524      0.792 0.988 0.000 0.004 0.008
#&gt; SRR1975491     2  0.3311      0.730 0.172 0.828 0.000 0.000
#&gt; SRR1975492     2  0.3311      0.730 0.172 0.828 0.000 0.000
#&gt; SRR1975489     1  0.7127      0.577 0.632 0.056 0.076 0.236
#&gt; SRR1975490     1  0.7127      0.577 0.632 0.056 0.076 0.236
#&gt; SRR1975487     1  0.6516      0.386 0.576 0.332 0.000 0.092
#&gt; SRR1975488     1  0.6516      0.386 0.576 0.332 0.000 0.092
#&gt; SRR1975485     1  0.6020      0.692 0.736 0.060 0.052 0.152
#&gt; SRR1975486     1  0.6065      0.690 0.732 0.060 0.052 0.156
#&gt; SRR1975483     1  0.0188      0.792 0.996 0.000 0.000 0.004
#&gt; SRR1975484     1  0.0188      0.792 0.996 0.000 0.000 0.004
#&gt; SRR1975481     1  0.1284      0.793 0.964 0.000 0.024 0.012
#&gt; SRR1975482     1  0.1284      0.793 0.964 0.000 0.024 0.012
#&gt; SRR1975477     4  0.5339      0.844 0.020 0.000 0.356 0.624
#&gt; SRR1975478     4  0.5339      0.844 0.020 0.000 0.356 0.624
#&gt; SRR1975479     4  0.7625      0.641 0.220 0.004 0.276 0.500
#&gt; SRR1975480     4  0.7625      0.641 0.220 0.004 0.276 0.500
#&gt; SRR1975475     1  0.7521      0.453 0.548 0.048 0.080 0.324
#&gt; SRR1975476     1  0.7505      0.451 0.552 0.048 0.080 0.320
#&gt; SRR1975473     4  0.5339      0.844 0.020 0.000 0.356 0.624
#&gt; SRR1975474     4  0.5339      0.844 0.020 0.000 0.356 0.624
#&gt; SRR1975471     1  0.2867      0.714 0.884 0.000 0.104 0.012
#&gt; SRR1975472     1  0.2867      0.714 0.884 0.000 0.104 0.012
#&gt; SRR1975469     1  0.0707      0.794 0.980 0.000 0.000 0.020
#&gt; SRR1975470     1  0.0707      0.794 0.980 0.000 0.000 0.020
#&gt; SRR1975467     2  0.1209      0.768 0.004 0.964 0.000 0.032
#&gt; SRR1975468     2  0.1209      0.768 0.004 0.964 0.000 0.032
#&gt; SRR1975465     2  0.4730      0.679 0.000 0.636 0.000 0.364
#&gt; SRR1975466     2  0.4730      0.679 0.000 0.636 0.000 0.364
#&gt; SRR1975463     2  0.4730      0.679 0.000 0.636 0.000 0.364
#&gt; SRR1975464     2  0.4730      0.679 0.000 0.636 0.000 0.364
#&gt; SRR1975461     3  0.0779      0.822 0.004 0.000 0.980 0.016
#&gt; SRR1975462     3  0.0779      0.822 0.004 0.000 0.980 0.016
#&gt; SRR1975459     2  0.4730      0.679 0.000 0.636 0.000 0.364
#&gt; SRR1975460     2  0.4730      0.679 0.000 0.636 0.000 0.364
#&gt; SRR1975457     4  0.5650      0.822 0.024 0.000 0.432 0.544
#&gt; SRR1975458     4  0.5650      0.822 0.024 0.000 0.432 0.544
#&gt; SRR1975455     4  0.5724      0.827 0.028 0.000 0.424 0.548
#&gt; SRR1975456     4  0.5724      0.827 0.028 0.000 0.424 0.548
#&gt; SRR1975453     3  0.4454      0.536 0.308 0.000 0.692 0.000
#&gt; SRR1975454     3  0.4454      0.536 0.308 0.000 0.692 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-3-a').click(function(){
  $('#tab-CV-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-4'>
<p><a id='tab-CV-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.0290      0.772 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1975507     3  0.0290      0.772 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1975506     3  0.0290      0.772 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1975505     3  0.0290      0.772 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1975503     4  0.7001      0.963 0.236 0.220 0.000 0.512 0.032
#&gt; SRR1975504     4  0.7001      0.963 0.236 0.220 0.000 0.512 0.032
#&gt; SRR1975501     4  0.7017      0.967 0.244 0.216 0.000 0.508 0.032
#&gt; SRR1975502     4  0.7017      0.967 0.244 0.216 0.000 0.508 0.032
#&gt; SRR1975499     4  0.7066      0.928 0.284 0.196 0.000 0.488 0.032
#&gt; SRR1975500     4  0.7066      0.928 0.284 0.196 0.000 0.488 0.032
#&gt; SRR1975497     1  0.2462      0.702 0.880 0.000 0.000 0.008 0.112
#&gt; SRR1975498     1  0.2411      0.704 0.884 0.000 0.000 0.008 0.108
#&gt; SRR1975493     2  0.4949      0.298 0.000 0.572 0.000 0.396 0.032
#&gt; SRR1975494     2  0.4949      0.298 0.000 0.572 0.000 0.396 0.032
#&gt; SRR1975495     1  0.0671      0.728 0.980 0.000 0.000 0.004 0.016
#&gt; SRR1975496     1  0.0566      0.727 0.984 0.000 0.000 0.004 0.012
#&gt; SRR1975491     4  0.6974      0.968 0.244 0.208 0.000 0.516 0.032
#&gt; SRR1975492     4  0.6974      0.968 0.244 0.208 0.000 0.516 0.032
#&gt; SRR1975489     1  0.6299      0.471 0.508 0.000 0.000 0.176 0.316
#&gt; SRR1975490     1  0.6299      0.471 0.508 0.000 0.000 0.176 0.316
#&gt; SRR1975487     1  0.6410      0.148 0.544 0.020 0.000 0.312 0.124
#&gt; SRR1975488     1  0.6410      0.148 0.544 0.020 0.000 0.312 0.124
#&gt; SRR1975485     1  0.5896      0.526 0.600 0.000 0.000 0.184 0.216
#&gt; SRR1975486     1  0.5867      0.531 0.604 0.000 0.000 0.180 0.216
#&gt; SRR1975483     1  0.0162      0.723 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1975484     1  0.0162      0.723 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1975481     1  0.1043      0.726 0.960 0.000 0.000 0.000 0.040
#&gt; SRR1975482     1  0.1043      0.726 0.960 0.000 0.000 0.000 0.040
#&gt; SRR1975477     5  0.0162      0.898 0.000 0.000 0.000 0.004 0.996
#&gt; SRR1975478     5  0.0162      0.898 0.000 0.000 0.000 0.004 0.996
#&gt; SRR1975479     5  0.1892      0.880 0.080 0.000 0.000 0.004 0.916
#&gt; SRR1975480     5  0.1892      0.880 0.080 0.000 0.000 0.004 0.916
#&gt; SRR1975475     1  0.6299      0.471 0.508 0.000 0.000 0.176 0.316
#&gt; SRR1975476     1  0.6299      0.471 0.508 0.000 0.000 0.176 0.316
#&gt; SRR1975473     5  0.0324      0.898 0.004 0.000 0.000 0.004 0.992
#&gt; SRR1975474     5  0.0324      0.898 0.004 0.000 0.000 0.004 0.992
#&gt; SRR1975471     1  0.0693      0.718 0.980 0.000 0.012 0.008 0.000
#&gt; SRR1975472     1  0.0693      0.718 0.980 0.000 0.012 0.008 0.000
#&gt; SRR1975469     1  0.0566      0.723 0.984 0.000 0.000 0.012 0.004
#&gt; SRR1975470     1  0.0566      0.723 0.984 0.000 0.000 0.012 0.004
#&gt; SRR1975467     2  0.4996      0.231 0.000 0.548 0.000 0.420 0.032
#&gt; SRR1975468     2  0.4996      0.231 0.000 0.548 0.000 0.420 0.032
#&gt; SRR1975465     2  0.0000      0.737 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.737 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.737 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.737 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975461     3  0.4302      0.769 0.000 0.000 0.520 0.480 0.000
#&gt; SRR1975462     3  0.4302      0.769 0.000 0.000 0.520 0.480 0.000
#&gt; SRR1975459     2  0.0000      0.737 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.737 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975457     5  0.3710      0.801 0.024 0.000 0.192 0.000 0.784
#&gt; SRR1975458     5  0.3710      0.801 0.024 0.000 0.192 0.000 0.784
#&gt; SRR1975455     5  0.2754      0.888 0.040 0.000 0.080 0.000 0.880
#&gt; SRR1975456     5  0.2754      0.888 0.040 0.000 0.080 0.000 0.880
#&gt; SRR1975453     3  0.4746      0.765 0.016 0.000 0.504 0.480 0.000
#&gt; SRR1975454     3  0.4746      0.765 0.016 0.000 0.504 0.480 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-4-a').click(function(){
  $('#tab-CV-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-5'>
<p><a id='tab-CV-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     3  0.0632     1.0000 0.000 0.000 0.976 0.000 0.000 0.024
#&gt; SRR1975507     3  0.0632     1.0000 0.000 0.000 0.976 0.000 0.000 0.024
#&gt; SRR1975506     3  0.0632     1.0000 0.000 0.000 0.976 0.000 0.000 0.024
#&gt; SRR1975505     3  0.0632     1.0000 0.000 0.000 0.976 0.000 0.000 0.024
#&gt; SRR1975503     4  0.2830     0.5929 0.020 0.144 0.000 0.836 0.000 0.000
#&gt; SRR1975504     4  0.2830     0.5929 0.020 0.144 0.000 0.836 0.000 0.000
#&gt; SRR1975501     4  0.2868     0.5989 0.028 0.132 0.000 0.840 0.000 0.000
#&gt; SRR1975502     4  0.2868     0.5989 0.028 0.132 0.000 0.840 0.000 0.000
#&gt; SRR1975499     4  0.3158     0.5980 0.064 0.084 0.008 0.844 0.000 0.000
#&gt; SRR1975500     4  0.3158     0.5980 0.064 0.084 0.008 0.844 0.000 0.000
#&gt; SRR1975497     1  0.1605     0.8437 0.936 0.000 0.004 0.016 0.044 0.000
#&gt; SRR1975498     1  0.1605     0.8437 0.936 0.000 0.004 0.016 0.044 0.000
#&gt; SRR1975493     4  0.3866     0.1793 0.000 0.484 0.000 0.516 0.000 0.000
#&gt; SRR1975494     4  0.3866     0.1793 0.000 0.484 0.000 0.516 0.000 0.000
#&gt; SRR1975495     1  0.1307     0.8741 0.952 0.000 0.008 0.032 0.008 0.000
#&gt; SRR1975496     1  0.1307     0.8741 0.952 0.000 0.008 0.032 0.008 0.000
#&gt; SRR1975491     4  0.2868     0.5989 0.028 0.132 0.000 0.840 0.000 0.000
#&gt; SRR1975492     4  0.2868     0.5989 0.028 0.132 0.000 0.840 0.000 0.000
#&gt; SRR1975489     4  0.5937    -0.0146 0.400 0.000 0.016 0.448 0.136 0.000
#&gt; SRR1975490     4  0.5937    -0.0146 0.400 0.000 0.016 0.448 0.136 0.000
#&gt; SRR1975487     4  0.3878     0.2977 0.320 0.000 0.008 0.668 0.004 0.000
#&gt; SRR1975488     4  0.3878     0.2977 0.320 0.000 0.008 0.668 0.004 0.000
#&gt; SRR1975485     1  0.4481     0.1935 0.556 0.000 0.004 0.416 0.024 0.000
#&gt; SRR1975486     1  0.4481     0.2013 0.556 0.000 0.004 0.416 0.024 0.000
#&gt; SRR1975483     1  0.0935     0.8728 0.964 0.000 0.000 0.032 0.004 0.000
#&gt; SRR1975484     1  0.0935     0.8728 0.964 0.000 0.000 0.032 0.004 0.000
#&gt; SRR1975481     1  0.2024     0.8406 0.920 0.000 0.016 0.028 0.036 0.000
#&gt; SRR1975482     1  0.2024     0.8406 0.920 0.000 0.016 0.028 0.036 0.000
#&gt; SRR1975477     5  0.0000     0.8350 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975478     5  0.0000     0.8350 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975479     5  0.4078     0.7726 0.072 0.000 0.016 0.140 0.772 0.000
#&gt; SRR1975480     5  0.4078     0.7726 0.072 0.000 0.016 0.140 0.772 0.000
#&gt; SRR1975475     4  0.5967    -0.0302 0.408 0.000 0.016 0.436 0.140 0.000
#&gt; SRR1975476     4  0.5967    -0.0302 0.408 0.000 0.016 0.436 0.140 0.000
#&gt; SRR1975473     5  0.0000     0.8350 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975474     5  0.0000     0.8350 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975471     1  0.1320     0.8697 0.948 0.000 0.016 0.036 0.000 0.000
#&gt; SRR1975472     1  0.1320     0.8697 0.948 0.000 0.016 0.036 0.000 0.000
#&gt; SRR1975469     1  0.0692     0.8729 0.976 0.000 0.004 0.020 0.000 0.000
#&gt; SRR1975470     1  0.0692     0.8729 0.976 0.000 0.004 0.020 0.000 0.000
#&gt; SRR1975467     4  0.3857     0.2167 0.000 0.468 0.000 0.532 0.000 0.000
#&gt; SRR1975468     4  0.3857     0.2167 0.000 0.468 0.000 0.532 0.000 0.000
#&gt; SRR1975465     2  0.0000     0.9981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000     0.9981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0146     0.9961 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1975464     2  0.0146     0.9961 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1975461     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975462     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975459     2  0.0000     0.9981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000     0.9981 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975457     5  0.4879     0.6865 0.040 0.000 0.000 0.036 0.660 0.264
#&gt; SRR1975458     5  0.4879     0.6865 0.040 0.000 0.000 0.036 0.660 0.264
#&gt; SRR1975455     5  0.3710     0.8276 0.056 0.000 0.004 0.036 0.824 0.080
#&gt; SRR1975456     5  0.3710     0.8276 0.056 0.000 0.004 0.036 0.824 0.080
#&gt; SRR1975453     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975454     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-5-a').click(function(){
  $('#tab-CV-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-mclust-signature_compare](figure_cola/CV-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-mclust-collect-classes](figure_cola/CV-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:NMF*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "NMF"]
# you can also extract it by
# res = res_list["CV:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-NMF-collect-plots](figure_cola/CV-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-NMF-select-partition-number](figure_cola/CV-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.998       0.999         0.4687 0.532   0.532
#> 3 3 1.000           0.982       0.985         0.3996 0.813   0.649
#> 4 4 0.917           0.966       0.951         0.1371 0.906   0.729
#> 5 5 0.807           0.682       0.824         0.0639 0.977   0.907
#> 6 6 0.782           0.661       0.781         0.0441 0.906   0.617
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-classes'>
<ul>
<li><a href='#tab-CV-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-NMF-get-classes-1'>
<p><a id='tab-CV-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975507     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975506     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975505     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975503     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975504     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975501     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975502     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975499     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975500     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975497     2  0.1414      0.980 0.020 0.980
#&gt; SRR1975498     2  0.2043      0.968 0.032 0.968
#&gt; SRR1975493     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975494     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975495     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975496     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975491     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975492     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975489     2  0.0376      0.995 0.004 0.996
#&gt; SRR1975490     2  0.0376      0.995 0.004 0.996
#&gt; SRR1975487     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975488     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975485     2  0.0672      0.992 0.008 0.992
#&gt; SRR1975486     2  0.0376      0.995 0.004 0.996
#&gt; SRR1975483     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975484     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975481     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975482     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975477     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975478     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975479     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975480     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975475     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975476     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975473     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975474     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975471     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975472     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975469     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975470     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975467     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975468     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975465     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975466     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975463     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975464     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975461     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975462     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975459     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975460     1  0.0000      1.000 1.000 0.000
#&gt; SRR1975457     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975458     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975455     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975456     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975453     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975454     2  0.0000      0.998 0.000 1.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-1-a').click(function(){
  $('#tab-CV-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-2'>
<p><a id='tab-CV-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2    p3
#&gt; SRR1975508     3   0.000      0.981 0.000  0 1.000
#&gt; SRR1975507     3   0.000      0.981 0.000  0 1.000
#&gt; SRR1975506     3   0.000      0.981 0.000  0 1.000
#&gt; SRR1975505     3   0.000      0.981 0.000  0 1.000
#&gt; SRR1975503     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975504     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975501     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975502     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975499     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975500     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975497     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975498     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975493     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975494     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975495     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975496     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975491     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975492     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975489     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975490     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975487     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975488     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975485     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975486     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975483     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975484     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975481     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975482     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975477     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975478     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975479     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975480     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975475     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975476     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975473     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975474     1   0.186      0.972 0.948  0 0.052
#&gt; SRR1975471     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975472     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975469     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975470     1   0.000      0.972 1.000  0 0.000
#&gt; SRR1975467     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975468     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975465     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975466     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975463     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975464     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975461     3   0.175      0.962 0.048  0 0.952
#&gt; SRR1975462     3   0.175      0.962 0.048  0 0.952
#&gt; SRR1975459     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975460     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1975457     3   0.000      0.981 0.000  0 1.000
#&gt; SRR1975458     3   0.000      0.981 0.000  0 1.000
#&gt; SRR1975455     3   0.000      0.981 0.000  0 1.000
#&gt; SRR1975456     3   0.000      0.981 0.000  0 1.000
#&gt; SRR1975453     3   0.186      0.959 0.052  0 0.948
#&gt; SRR1975454     3   0.186      0.959 0.052  0 0.948
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-2-a').click(function(){
  $('#tab-CV-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-3'>
<p><a id='tab-CV-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR1975507     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR1975506     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR1975505     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR1975503     2  0.1398      0.981 0.040 0.956 0.000 0.004
#&gt; SRR1975504     2  0.1398      0.981 0.040 0.956 0.000 0.004
#&gt; SRR1975501     2  0.0817      0.984 0.024 0.976 0.000 0.000
#&gt; SRR1975502     2  0.0817      0.984 0.024 0.976 0.000 0.000
#&gt; SRR1975499     2  0.1398      0.981 0.040 0.956 0.000 0.004
#&gt; SRR1975500     2  0.1398      0.981 0.040 0.956 0.000 0.004
#&gt; SRR1975497     1  0.1211      0.916 0.960 0.000 0.000 0.040
#&gt; SRR1975498     1  0.1211      0.916 0.960 0.000 0.000 0.040
#&gt; SRR1975493     2  0.0469      0.984 0.012 0.988 0.000 0.000
#&gt; SRR1975494     2  0.0469      0.984 0.012 0.988 0.000 0.000
#&gt; SRR1975495     1  0.1389      0.919 0.952 0.000 0.000 0.048
#&gt; SRR1975496     1  0.1389      0.919 0.952 0.000 0.000 0.048
#&gt; SRR1975491     2  0.1118      0.983 0.036 0.964 0.000 0.000
#&gt; SRR1975492     2  0.1118      0.983 0.036 0.964 0.000 0.000
#&gt; SRR1975489     4  0.0000      0.952 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4  0.0000      0.952 0.000 0.000 0.000 1.000
#&gt; SRR1975487     2  0.1545      0.980 0.040 0.952 0.000 0.008
#&gt; SRR1975488     2  0.1677      0.977 0.040 0.948 0.000 0.012
#&gt; SRR1975485     4  0.2589      0.910 0.116 0.000 0.000 0.884
#&gt; SRR1975486     4  0.2589      0.910 0.116 0.000 0.000 0.884
#&gt; SRR1975483     1  0.2760      0.951 0.872 0.000 0.000 0.128
#&gt; SRR1975484     1  0.2760      0.951 0.872 0.000 0.000 0.128
#&gt; SRR1975481     1  0.2760      0.951 0.872 0.000 0.000 0.128
#&gt; SRR1975482     1  0.2760      0.951 0.872 0.000 0.000 0.128
#&gt; SRR1975477     4  0.0188      0.954 0.004 0.000 0.000 0.996
#&gt; SRR1975478     4  0.0188      0.954 0.004 0.000 0.000 0.996
#&gt; SRR1975479     4  0.0188      0.954 0.004 0.000 0.000 0.996
#&gt; SRR1975480     4  0.0188      0.954 0.004 0.000 0.000 0.996
#&gt; SRR1975475     4  0.2589      0.910 0.116 0.000 0.000 0.884
#&gt; SRR1975476     4  0.2589      0.910 0.116 0.000 0.000 0.884
#&gt; SRR1975473     4  0.0188      0.954 0.004 0.000 0.000 0.996
#&gt; SRR1975474     4  0.0188      0.954 0.004 0.000 0.000 0.996
#&gt; SRR1975471     1  0.3123      0.939 0.844 0.000 0.000 0.156
#&gt; SRR1975472     1  0.3123      0.939 0.844 0.000 0.000 0.156
#&gt; SRR1975469     1  0.3172      0.939 0.840 0.000 0.000 0.160
#&gt; SRR1975470     1  0.3172      0.939 0.840 0.000 0.000 0.160
#&gt; SRR1975467     2  0.0000      0.984 0.000 1.000 0.000 0.000
#&gt; SRR1975468     2  0.0000      0.984 0.000 1.000 0.000 0.000
#&gt; SRR1975465     2  0.0000      0.984 0.000 1.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.984 0.000 1.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.984 0.000 1.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.984 0.000 1.000 0.000 0.000
#&gt; SRR1975461     3  0.0336      0.996 0.008 0.000 0.992 0.000
#&gt; SRR1975462     3  0.0336      0.996 0.008 0.000 0.992 0.000
#&gt; SRR1975459     2  0.0000      0.984 0.000 1.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.984 0.000 1.000 0.000 0.000
#&gt; SRR1975457     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR1975458     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR1975455     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR1975456     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR1975453     3  0.0336      0.996 0.008 0.000 0.992 0.000
#&gt; SRR1975454     3  0.0336      0.996 0.008 0.000 0.992 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-3-a').click(function(){
  $('#tab-CV-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-4'>
<p><a id='tab-CV-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.0000      0.920 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975507     3  0.0000      0.920 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975506     3  0.0000      0.920 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975505     3  0.0000      0.920 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975503     2  0.4273     -0.654 0.000 0.552 0.000 0.000 0.448
#&gt; SRR1975504     2  0.4273     -0.654 0.000 0.552 0.000 0.000 0.448
#&gt; SRR1975501     2  0.2488      0.579 0.004 0.872 0.000 0.000 0.124
#&gt; SRR1975502     2  0.2536      0.574 0.004 0.868 0.000 0.000 0.128
#&gt; SRR1975499     2  0.4287     -0.643 0.000 0.540 0.000 0.000 0.460
#&gt; SRR1975500     2  0.4287     -0.643 0.000 0.540 0.000 0.000 0.460
#&gt; SRR1975497     1  0.2763      0.824 0.848 0.000 0.000 0.004 0.148
#&gt; SRR1975498     1  0.2763      0.824 0.848 0.000 0.000 0.004 0.148
#&gt; SRR1975493     2  0.2732      0.498 0.000 0.840 0.000 0.000 0.160
#&gt; SRR1975494     2  0.2732      0.498 0.000 0.840 0.000 0.000 0.160
#&gt; SRR1975495     1  0.2674      0.827 0.856 0.000 0.000 0.004 0.140
#&gt; SRR1975496     1  0.2674      0.827 0.856 0.000 0.000 0.004 0.140
#&gt; SRR1975491     2  0.3752      0.298 0.000 0.708 0.000 0.000 0.292
#&gt; SRR1975492     2  0.3774      0.292 0.000 0.704 0.000 0.000 0.296
#&gt; SRR1975489     4  0.1608      0.868 0.000 0.000 0.000 0.928 0.072
#&gt; SRR1975490     4  0.1608      0.868 0.000 0.000 0.000 0.928 0.072
#&gt; SRR1975487     5  0.4641      0.970 0.000 0.456 0.000 0.012 0.532
#&gt; SRR1975488     5  0.4807      0.970 0.000 0.448 0.000 0.020 0.532
#&gt; SRR1975485     4  0.5625      0.739 0.084 0.000 0.012 0.632 0.272
#&gt; SRR1975486     4  0.5625      0.739 0.084 0.000 0.012 0.632 0.272
#&gt; SRR1975483     1  0.1965      0.869 0.924 0.000 0.000 0.052 0.024
#&gt; SRR1975484     1  0.1965      0.869 0.924 0.000 0.000 0.052 0.024
#&gt; SRR1975481     1  0.2054      0.869 0.920 0.000 0.000 0.052 0.028
#&gt; SRR1975482     1  0.2054      0.869 0.920 0.000 0.000 0.052 0.028
#&gt; SRR1975477     4  0.0290      0.877 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975478     4  0.0290      0.877 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975479     4  0.0290      0.876 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975480     4  0.0290      0.876 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1975475     4  0.5336      0.768 0.080 0.000 0.012 0.676 0.232
#&gt; SRR1975476     4  0.5336      0.768 0.080 0.000 0.012 0.676 0.232
#&gt; SRR1975473     4  0.0162      0.876 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1975474     4  0.0162      0.876 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1975471     1  0.4298      0.810 0.756 0.000 0.000 0.060 0.184
#&gt; SRR1975472     1  0.4298      0.810 0.756 0.000 0.000 0.060 0.184
#&gt; SRR1975469     1  0.3875      0.836 0.804 0.000 0.000 0.072 0.124
#&gt; SRR1975470     1  0.3875      0.836 0.804 0.000 0.000 0.072 0.124
#&gt; SRR1975467     2  0.0000      0.668 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975468     2  0.0000      0.668 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975465     2  0.0000      0.668 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.668 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.668 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.668 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975461     3  0.3635      0.831 0.004 0.000 0.748 0.000 0.248
#&gt; SRR1975462     3  0.3635      0.831 0.004 0.000 0.748 0.000 0.248
#&gt; SRR1975459     2  0.0000      0.668 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.668 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975457     3  0.0290      0.919 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1975458     3  0.0290      0.919 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1975455     3  0.0000      0.920 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975456     3  0.0000      0.920 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975453     3  0.3863      0.825 0.012 0.000 0.740 0.000 0.248
#&gt; SRR1975454     3  0.3863      0.825 0.012 0.000 0.740 0.000 0.248
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-4-a').click(function(){
  $('#tab-CV-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-5'>
<p><a id='tab-CV-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     5  0.0000      0.978 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975507     5  0.0000      0.978 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975506     5  0.0000      0.978 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975505     5  0.0000      0.978 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975503     6  0.3636      0.874 0.000 0.320 0.004 0.000 0.000 0.676
#&gt; SRR1975504     6  0.3636      0.874 0.000 0.320 0.004 0.000 0.000 0.676
#&gt; SRR1975501     2  0.3916      0.693 0.084 0.804 0.040 0.000 0.000 0.072
#&gt; SRR1975502     2  0.3916      0.693 0.084 0.804 0.040 0.000 0.000 0.072
#&gt; SRR1975499     6  0.3922      0.861 0.000 0.320 0.016 0.000 0.000 0.664
#&gt; SRR1975500     6  0.3922      0.861 0.000 0.320 0.016 0.000 0.000 0.664
#&gt; SRR1975497     1  0.0146      0.691 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1975498     1  0.0146      0.691 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1975493     2  0.3720      0.521 0.000 0.736 0.028 0.000 0.000 0.236
#&gt; SRR1975494     2  0.3720      0.521 0.000 0.736 0.028 0.000 0.000 0.236
#&gt; SRR1975495     1  0.0717      0.693 0.976 0.000 0.016 0.000 0.000 0.008
#&gt; SRR1975496     1  0.0717      0.693 0.976 0.000 0.016 0.000 0.000 0.008
#&gt; SRR1975491     2  0.5262      0.254 0.024 0.576 0.060 0.000 0.000 0.340
#&gt; SRR1975492     2  0.5262      0.254 0.024 0.576 0.060 0.000 0.000 0.340
#&gt; SRR1975489     4  0.3204      0.747 0.004 0.000 0.032 0.820 0.000 0.144
#&gt; SRR1975490     4  0.3204      0.747 0.004 0.000 0.032 0.820 0.000 0.144
#&gt; SRR1975487     6  0.3261      0.816 0.004 0.192 0.004 0.008 0.000 0.792
#&gt; SRR1975488     6  0.3261      0.816 0.004 0.192 0.004 0.008 0.000 0.792
#&gt; SRR1975485     4  0.6791      0.544 0.216 0.000 0.056 0.428 0.000 0.300
#&gt; SRR1975486     4  0.6791      0.544 0.216 0.000 0.056 0.428 0.000 0.300
#&gt; SRR1975483     1  0.4871      0.651 0.592 0.000 0.352 0.016 0.000 0.040
#&gt; SRR1975484     1  0.4871      0.651 0.592 0.000 0.352 0.016 0.000 0.040
#&gt; SRR1975481     1  0.5001      0.629 0.560 0.000 0.380 0.016 0.000 0.044
#&gt; SRR1975482     1  0.5001      0.629 0.560 0.000 0.380 0.016 0.000 0.044
#&gt; SRR1975477     4  0.0909      0.775 0.000 0.000 0.020 0.968 0.000 0.012
#&gt; SRR1975478     4  0.0909      0.775 0.000 0.000 0.020 0.968 0.000 0.012
#&gt; SRR1975479     4  0.1176      0.775 0.000 0.000 0.024 0.956 0.000 0.020
#&gt; SRR1975480     4  0.1176      0.775 0.000 0.000 0.024 0.956 0.000 0.020
#&gt; SRR1975475     4  0.6498      0.570 0.228 0.000 0.044 0.492 0.000 0.236
#&gt; SRR1975476     4  0.6498      0.570 0.228 0.000 0.044 0.492 0.000 0.236
#&gt; SRR1975473     4  0.0972      0.771 0.000 0.000 0.028 0.964 0.000 0.008
#&gt; SRR1975474     4  0.0972      0.771 0.000 0.000 0.028 0.964 0.000 0.008
#&gt; SRR1975471     3  0.3342      0.161 0.228 0.000 0.760 0.012 0.000 0.000
#&gt; SRR1975472     3  0.3342      0.161 0.228 0.000 0.760 0.012 0.000 0.000
#&gt; SRR1975469     3  0.4858     -0.201 0.364 0.000 0.584 0.032 0.000 0.020
#&gt; SRR1975470     3  0.4858     -0.201 0.364 0.000 0.584 0.032 0.000 0.020
#&gt; SRR1975467     2  0.0260      0.816 0.000 0.992 0.008 0.000 0.000 0.000
#&gt; SRR1975468     2  0.0260      0.816 0.000 0.992 0.008 0.000 0.000 0.000
#&gt; SRR1975465     2  0.0000      0.818 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.818 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.818 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.818 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975461     3  0.5184      0.268 0.000 0.000 0.480 0.000 0.432 0.088
#&gt; SRR1975462     3  0.5184      0.268 0.000 0.000 0.480 0.000 0.432 0.088
#&gt; SRR1975459     2  0.0000      0.818 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.818 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975457     5  0.1003      0.963 0.000 0.000 0.016 0.000 0.964 0.020
#&gt; SRR1975458     5  0.1003      0.963 0.000 0.000 0.016 0.000 0.964 0.020
#&gt; SRR1975455     5  0.0976      0.960 0.000 0.000 0.016 0.008 0.968 0.008
#&gt; SRR1975456     5  0.0976      0.960 0.000 0.000 0.016 0.008 0.968 0.008
#&gt; SRR1975453     3  0.5310      0.275 0.004 0.000 0.480 0.000 0.428 0.088
#&gt; SRR1975454     3  0.5310      0.275 0.004 0.000 0.480 0.000 0.428 0.088
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-5-a').click(function(){
  $('#tab-CV-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-NMF-signature_compare](figure_cola/CV-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-CV-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-NMF-collect-classes](figure_cola/CV-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "hclust"]
# you can also extract it by
# res = res_list["MAD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-hclust-collect-plots](figure_cola/MAD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-hclust-select-partition-number](figure_cola/MAD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.852           0.957       0.972         0.4208 0.584   0.584
#> 3 3 0.642           0.806       0.864         0.5334 0.764   0.596
#> 4 4 0.748           0.589       0.788         0.1543 0.969   0.910
#> 5 5 0.730           0.659       0.778         0.0602 0.940   0.813
#> 6 6 0.807           0.792       0.851         0.0339 0.917   0.683
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-classes'>
<ul>
<li><a href='#tab-MAD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-hclust-get-classes-1'>
<p><a id='tab-MAD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975507     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975506     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975505     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975503     1  0.2236      0.952 0.964 0.036
#&gt; SRR1975504     1  0.2236      0.952 0.964 0.036
#&gt; SRR1975501     2  0.3733      0.939 0.072 0.928
#&gt; SRR1975502     2  0.3733      0.939 0.072 0.928
#&gt; SRR1975499     1  0.0000      0.973 1.000 0.000
#&gt; SRR1975500     1  0.0000      0.973 1.000 0.000
#&gt; SRR1975497     2  0.4815      0.912 0.104 0.896
#&gt; SRR1975498     2  0.4815      0.912 0.104 0.896
#&gt; SRR1975493     2  0.2603      0.958 0.044 0.956
#&gt; SRR1975494     2  0.2603      0.958 0.044 0.956
#&gt; SRR1975495     2  0.0376      0.971 0.004 0.996
#&gt; SRR1975496     2  0.0376      0.971 0.004 0.996
#&gt; SRR1975491     2  0.5059      0.905 0.112 0.888
#&gt; SRR1975492     2  0.5059      0.905 0.112 0.888
#&gt; SRR1975489     1  0.0000      0.973 1.000 0.000
#&gt; SRR1975490     1  0.0000      0.973 1.000 0.000
#&gt; SRR1975487     1  0.0000      0.973 1.000 0.000
#&gt; SRR1975488     1  0.0000      0.973 1.000 0.000
#&gt; SRR1975485     1  0.0000      0.973 1.000 0.000
#&gt; SRR1975486     1  0.0000      0.973 1.000 0.000
#&gt; SRR1975483     2  0.0376      0.971 0.004 0.996
#&gt; SRR1975484     2  0.0376      0.971 0.004 0.996
#&gt; SRR1975481     2  0.0376      0.971 0.004 0.996
#&gt; SRR1975482     2  0.0376      0.971 0.004 0.996
#&gt; SRR1975477     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975478     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975479     1  0.0000      0.973 1.000 0.000
#&gt; SRR1975480     1  0.0000      0.973 1.000 0.000
#&gt; SRR1975475     1  0.0376      0.972 0.996 0.004
#&gt; SRR1975476     1  0.0376      0.972 0.996 0.004
#&gt; SRR1975473     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975474     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975471     2  0.0376      0.971 0.004 0.996
#&gt; SRR1975472     2  0.0376      0.971 0.004 0.996
#&gt; SRR1975469     2  0.4562      0.920 0.096 0.904
#&gt; SRR1975470     2  0.4562      0.920 0.096 0.904
#&gt; SRR1975467     1  0.6247      0.834 0.844 0.156
#&gt; SRR1975468     1  0.6247      0.834 0.844 0.156
#&gt; SRR1975465     2  0.2603      0.958 0.044 0.956
#&gt; SRR1975466     2  0.2603      0.958 0.044 0.956
#&gt; SRR1975463     2  0.2603      0.958 0.044 0.956
#&gt; SRR1975464     2  0.2603      0.958 0.044 0.956
#&gt; SRR1975461     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975462     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975459     2  0.2603      0.958 0.044 0.956
#&gt; SRR1975460     2  0.2603      0.958 0.044 0.956
#&gt; SRR1975457     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975458     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975455     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975456     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975453     2  0.0000      0.971 0.000 1.000
#&gt; SRR1975454     2  0.0000      0.971 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-1-a').click(function(){
  $('#tab-MAD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-2'>
<p><a id='tab-MAD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     2  0.4931      0.798 0.000 0.768 0.232
#&gt; SRR1975507     2  0.4931      0.798 0.000 0.768 0.232
#&gt; SRR1975506     2  0.4931      0.798 0.000 0.768 0.232
#&gt; SRR1975505     2  0.4931      0.798 0.000 0.768 0.232
#&gt; SRR1975503     1  0.2926      0.925 0.924 0.040 0.036
#&gt; SRR1975504     1  0.2926      0.925 0.924 0.040 0.036
#&gt; SRR1975501     3  0.7425      0.516 0.052 0.328 0.620
#&gt; SRR1975502     3  0.7425      0.516 0.052 0.328 0.620
#&gt; SRR1975499     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR1975500     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR1975497     3  0.2711      0.852 0.088 0.000 0.912
#&gt; SRR1975498     3  0.2711      0.852 0.088 0.000 0.912
#&gt; SRR1975493     2  0.1411      0.741 0.000 0.964 0.036
#&gt; SRR1975494     2  0.1411      0.741 0.000 0.964 0.036
#&gt; SRR1975495     3  0.0592      0.891 0.000 0.012 0.988
#&gt; SRR1975496     3  0.0592      0.891 0.000 0.012 0.988
#&gt; SRR1975491     2  0.8465      0.175 0.096 0.528 0.376
#&gt; SRR1975492     2  0.8465      0.175 0.096 0.528 0.376
#&gt; SRR1975489     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR1975490     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR1975487     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR1975488     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR1975485     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR1975486     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR1975483     3  0.0592      0.891 0.000 0.012 0.988
#&gt; SRR1975484     3  0.0592      0.891 0.000 0.012 0.988
#&gt; SRR1975481     3  0.0592      0.891 0.000 0.012 0.988
#&gt; SRR1975482     3  0.0592      0.891 0.000 0.012 0.988
#&gt; SRR1975477     2  0.5216      0.805 0.000 0.740 0.260
#&gt; SRR1975478     2  0.5216      0.805 0.000 0.740 0.260
#&gt; SRR1975479     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR1975480     1  0.0000      0.960 1.000 0.000 0.000
#&gt; SRR1975475     1  0.1765      0.945 0.956 0.040 0.004
#&gt; SRR1975476     1  0.1765      0.945 0.956 0.040 0.004
#&gt; SRR1975473     2  0.5216      0.805 0.000 0.740 0.260
#&gt; SRR1975474     2  0.5216      0.805 0.000 0.740 0.260
#&gt; SRR1975471     3  0.0592      0.891 0.000 0.012 0.988
#&gt; SRR1975472     3  0.0592      0.891 0.000 0.012 0.988
#&gt; SRR1975469     3  0.3129      0.857 0.088 0.008 0.904
#&gt; SRR1975470     3  0.3129      0.857 0.088 0.008 0.904
#&gt; SRR1975467     1  0.5413      0.827 0.800 0.164 0.036
#&gt; SRR1975468     1  0.5413      0.827 0.800 0.164 0.036
#&gt; SRR1975465     2  0.1411      0.741 0.000 0.964 0.036
#&gt; SRR1975466     2  0.1411      0.741 0.000 0.964 0.036
#&gt; SRR1975463     2  0.1411      0.741 0.000 0.964 0.036
#&gt; SRR1975464     2  0.1411      0.741 0.000 0.964 0.036
#&gt; SRR1975461     2  0.6008      0.669 0.000 0.628 0.372
#&gt; SRR1975462     2  0.6008      0.669 0.000 0.628 0.372
#&gt; SRR1975459     2  0.1411      0.741 0.000 0.964 0.036
#&gt; SRR1975460     2  0.1411      0.741 0.000 0.964 0.036
#&gt; SRR1975457     2  0.5216      0.805 0.000 0.740 0.260
#&gt; SRR1975458     2  0.5216      0.805 0.000 0.740 0.260
#&gt; SRR1975455     2  0.5216      0.805 0.000 0.740 0.260
#&gt; SRR1975456     2  0.5216      0.805 0.000 0.740 0.260
#&gt; SRR1975453     2  0.6008      0.669 0.000 0.628 0.372
#&gt; SRR1975454     2  0.6008      0.669 0.000 0.628 0.372
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-2-a').click(function(){
  $('#tab-MAD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-3'>
<p><a id='tab-MAD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3   0.450     0.4929 0.000 0.316 0.684 0.000
#&gt; SRR1975507     3   0.450     0.4929 0.000 0.316 0.684 0.000
#&gt; SRR1975506     3   0.450     0.4929 0.000 0.316 0.684 0.000
#&gt; SRR1975505     3   0.450     0.4929 0.000 0.316 0.684 0.000
#&gt; SRR1975503     4   0.312     0.9004 0.000 0.092 0.028 0.880
#&gt; SRR1975504     4   0.312     0.9004 0.000 0.092 0.028 0.880
#&gt; SRR1975501     1   0.499    -0.2270 0.520 0.480 0.000 0.000
#&gt; SRR1975502     1   0.499    -0.2270 0.520 0.480 0.000 0.000
#&gt; SRR1975499     4   0.000     0.9383 0.000 0.000 0.000 1.000
#&gt; SRR1975500     4   0.000     0.9383 0.000 0.000 0.000 1.000
#&gt; SRR1975497     1   0.307     0.6746 0.848 0.152 0.000 0.000
#&gt; SRR1975498     1   0.307     0.6746 0.848 0.152 0.000 0.000
#&gt; SRR1975493     3   0.500    -0.0328 0.000 0.488 0.512 0.000
#&gt; SRR1975494     3   0.500    -0.0328 0.000 0.488 0.512 0.000
#&gt; SRR1975495     1   0.208     0.8021 0.916 0.000 0.084 0.000
#&gt; SRR1975496     1   0.208     0.8021 0.916 0.000 0.084 0.000
#&gt; SRR1975491     2   0.687     1.0000 0.240 0.592 0.168 0.000
#&gt; SRR1975492     2   0.687     1.0000 0.240 0.592 0.168 0.000
#&gt; SRR1975489     4   0.000     0.9383 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4   0.000     0.9383 0.000 0.000 0.000 1.000
#&gt; SRR1975487     4   0.000     0.9383 0.000 0.000 0.000 1.000
#&gt; SRR1975488     4   0.000     0.9383 0.000 0.000 0.000 1.000
#&gt; SRR1975485     4   0.000     0.9383 0.000 0.000 0.000 1.000
#&gt; SRR1975486     4   0.000     0.9383 0.000 0.000 0.000 1.000
#&gt; SRR1975483     1   0.208     0.8021 0.916 0.000 0.084 0.000
#&gt; SRR1975484     1   0.208     0.8021 0.916 0.000 0.084 0.000
#&gt; SRR1975481     1   0.208     0.8021 0.916 0.000 0.084 0.000
#&gt; SRR1975482     1   0.208     0.8021 0.916 0.000 0.084 0.000
#&gt; SRR1975477     3   0.000     0.5516 0.000 0.000 1.000 0.000
#&gt; SRR1975478     3   0.000     0.5516 0.000 0.000 1.000 0.000
#&gt; SRR1975479     4   0.130     0.9317 0.000 0.044 0.000 0.956
#&gt; SRR1975480     4   0.130     0.9317 0.000 0.044 0.000 0.956
#&gt; SRR1975475     4   0.227     0.9201 0.000 0.084 0.004 0.912
#&gt; SRR1975476     4   0.227     0.9201 0.000 0.084 0.004 0.912
#&gt; SRR1975473     3   0.000     0.5516 0.000 0.000 1.000 0.000
#&gt; SRR1975474     3   0.000     0.5516 0.000 0.000 1.000 0.000
#&gt; SRR1975471     1   0.208     0.8021 0.916 0.000 0.084 0.000
#&gt; SRR1975472     1   0.208     0.8021 0.916 0.000 0.084 0.000
#&gt; SRR1975469     1   0.265     0.7026 0.880 0.120 0.000 0.000
#&gt; SRR1975470     1   0.265     0.7026 0.880 0.120 0.000 0.000
#&gt; SRR1975467     4   0.464     0.7724 0.000 0.216 0.028 0.756
#&gt; SRR1975468     4   0.464     0.7724 0.000 0.216 0.028 0.756
#&gt; SRR1975465     3   0.500    -0.0328 0.000 0.488 0.512 0.000
#&gt; SRR1975466     3   0.500    -0.0328 0.000 0.488 0.512 0.000
#&gt; SRR1975463     3   0.500    -0.0328 0.000 0.488 0.512 0.000
#&gt; SRR1975464     3   0.500    -0.0328 0.000 0.488 0.512 0.000
#&gt; SRR1975461     3   0.711     0.3999 0.152 0.316 0.532 0.000
#&gt; SRR1975462     3   0.711     0.3999 0.152 0.316 0.532 0.000
#&gt; SRR1975459     3   0.500    -0.0328 0.000 0.488 0.512 0.000
#&gt; SRR1975460     3   0.500    -0.0328 0.000 0.488 0.512 0.000
#&gt; SRR1975457     3   0.000     0.5516 0.000 0.000 1.000 0.000
#&gt; SRR1975458     3   0.000     0.5516 0.000 0.000 1.000 0.000
#&gt; SRR1975455     3   0.000     0.5516 0.000 0.000 1.000 0.000
#&gt; SRR1975456     3   0.000     0.5516 0.000 0.000 1.000 0.000
#&gt; SRR1975453     3   0.728     0.3858 0.172 0.316 0.512 0.000
#&gt; SRR1975454     3   0.728     0.3858 0.172 0.316 0.512 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-3-a').click(function(){
  $('#tab-MAD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-4'>
<p><a id='tab-MAD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.4060      0.467 0.000 0.000 0.640 0.360 0.000
#&gt; SRR1975507     3  0.4060      0.467 0.000 0.000 0.640 0.360 0.000
#&gt; SRR1975506     3  0.4060      0.467 0.000 0.000 0.640 0.360 0.000
#&gt; SRR1975505     3  0.4060      0.467 0.000 0.000 0.640 0.360 0.000
#&gt; SRR1975503     5  0.0000      0.911 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975504     5  0.0000      0.911 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975501     2  0.6100      0.559 0.428 0.448 0.000 0.124 0.000
#&gt; SRR1975502     2  0.6100      0.559 0.428 0.448 0.000 0.124 0.000
#&gt; SRR1975499     4  0.6050      0.996 0.000 0.360 0.000 0.512 0.128
#&gt; SRR1975500     4  0.6050      0.996 0.000 0.360 0.000 0.512 0.128
#&gt; SRR1975497     1  0.3656      0.650 0.800 0.168 0.000 0.032 0.000
#&gt; SRR1975498     1  0.3656      0.650 0.800 0.168 0.000 0.032 0.000
#&gt; SRR1975493     3  0.5165      0.244 0.000 0.448 0.512 0.000 0.040
#&gt; SRR1975494     3  0.5165      0.244 0.000 0.448 0.512 0.000 0.040
#&gt; SRR1975495     1  0.0963      0.872 0.964 0.000 0.036 0.000 0.000
#&gt; SRR1975496     1  0.0963      0.872 0.964 0.000 0.036 0.000 0.000
#&gt; SRR1975491     2  0.8469      0.710 0.148 0.508 0.140 0.124 0.080
#&gt; SRR1975492     2  0.8469      0.710 0.148 0.508 0.140 0.124 0.080
#&gt; SRR1975489     4  0.6015      0.999 0.000 0.360 0.000 0.516 0.124
#&gt; SRR1975490     4  0.6015      0.999 0.000 0.360 0.000 0.516 0.124
#&gt; SRR1975487     4  0.6015      0.999 0.000 0.360 0.000 0.516 0.124
#&gt; SRR1975488     4  0.6015      0.999 0.000 0.360 0.000 0.516 0.124
#&gt; SRR1975485     4  0.6015      0.999 0.000 0.360 0.000 0.516 0.124
#&gt; SRR1975486     4  0.6015      0.999 0.000 0.360 0.000 0.516 0.124
#&gt; SRR1975483     1  0.0963      0.872 0.964 0.000 0.036 0.000 0.000
#&gt; SRR1975484     1  0.0963      0.872 0.964 0.000 0.036 0.000 0.000
#&gt; SRR1975481     1  0.0963      0.872 0.964 0.000 0.036 0.000 0.000
#&gt; SRR1975482     1  0.0963      0.872 0.964 0.000 0.036 0.000 0.000
#&gt; SRR1975477     3  0.0000      0.570 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975478     3  0.0000      0.570 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975479     5  0.1981      0.877 0.000 0.028 0.000 0.048 0.924
#&gt; SRR1975480     5  0.1981      0.877 0.000 0.028 0.000 0.048 0.924
#&gt; SRR1975475     5  0.0992      0.911 0.000 0.024 0.000 0.008 0.968
#&gt; SRR1975476     5  0.0992      0.911 0.000 0.024 0.000 0.008 0.968
#&gt; SRR1975473     3  0.0000      0.570 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975474     3  0.0000      0.570 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975471     1  0.0963      0.872 0.964 0.000 0.036 0.000 0.000
#&gt; SRR1975472     1  0.0963      0.872 0.964 0.000 0.036 0.000 0.000
#&gt; SRR1975469     1  0.3321      0.700 0.832 0.136 0.000 0.032 0.000
#&gt; SRR1975470     1  0.3321      0.700 0.832 0.136 0.000 0.032 0.000
#&gt; SRR1975467     5  0.2329      0.813 0.000 0.124 0.000 0.000 0.876
#&gt; SRR1975468     5  0.2329      0.813 0.000 0.124 0.000 0.000 0.876
#&gt; SRR1975465     3  0.5165      0.244 0.000 0.448 0.512 0.000 0.040
#&gt; SRR1975466     3  0.5165      0.244 0.000 0.448 0.512 0.000 0.040
#&gt; SRR1975463     3  0.5165      0.244 0.000 0.448 0.512 0.000 0.040
#&gt; SRR1975464     3  0.5165      0.244 0.000 0.448 0.512 0.000 0.040
#&gt; SRR1975461     3  0.6510      0.332 0.196 0.000 0.444 0.360 0.000
#&gt; SRR1975462     3  0.6510      0.332 0.196 0.000 0.444 0.360 0.000
#&gt; SRR1975459     3  0.5165      0.244 0.000 0.448 0.512 0.000 0.040
#&gt; SRR1975460     3  0.5165      0.244 0.000 0.448 0.512 0.000 0.040
#&gt; SRR1975457     3  0.0000      0.570 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975458     3  0.0000      0.570 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975455     3  0.0000      0.570 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975456     3  0.0000      0.570 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975453     3  0.6619      0.312 0.220 0.000 0.420 0.360 0.000
#&gt; SRR1975454     3  0.6619      0.312 0.220 0.000 0.420 0.360 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-4-a').click(function(){
  $('#tab-MAD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-5'>
<p><a id='tab-MAD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     5   0.176      0.615 0.000 0.096 0.000 0.000 0.904 0.000
#&gt; SRR1975507     5   0.176      0.615 0.000 0.096 0.000 0.000 0.904 0.000
#&gt; SRR1975506     5   0.176      0.615 0.000 0.096 0.000 0.000 0.904 0.000
#&gt; SRR1975505     5   0.176      0.615 0.000 0.096 0.000 0.000 0.904 0.000
#&gt; SRR1975503     3   0.254      0.911 0.000 0.012 0.864 0.120 0.000 0.004
#&gt; SRR1975504     3   0.254      0.911 0.000 0.012 0.864 0.120 0.000 0.004
#&gt; SRR1975501     6   0.355      0.775 0.192 0.036 0.000 0.000 0.000 0.772
#&gt; SRR1975502     6   0.355      0.775 0.192 0.036 0.000 0.000 0.000 0.772
#&gt; SRR1975499     4   0.026      0.992 0.000 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1975500     4   0.026      0.992 0.000 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1975497     1   0.527      0.645 0.672 0.000 0.044 0.000 0.096 0.188
#&gt; SRR1975498     1   0.527      0.645 0.672 0.000 0.044 0.000 0.096 0.188
#&gt; SRR1975493     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975494     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975495     1   0.000      0.888 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975496     1   0.000      0.888 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975491     6   0.246      0.800 0.000 0.096 0.028 0.000 0.000 0.876
#&gt; SRR1975492     6   0.246      0.800 0.000 0.096 0.028 0.000 0.000 0.876
#&gt; SRR1975489     4   0.000      0.997 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975490     4   0.000      0.997 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975487     4   0.000      0.997 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975488     4   0.000      0.997 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975485     4   0.000      0.997 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975486     4   0.000      0.997 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975483     1   0.000      0.888 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975484     1   0.000      0.888 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975481     1   0.000      0.888 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975482     1   0.000      0.888 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975477     5   0.385      0.522 0.000 0.456 0.000 0.000 0.544 0.000
#&gt; SRR1975478     5   0.385      0.522 0.000 0.456 0.000 0.000 0.544 0.000
#&gt; SRR1975479     3   0.263      0.891 0.000 0.000 0.820 0.180 0.000 0.000
#&gt; SRR1975480     3   0.263      0.891 0.000 0.000 0.820 0.180 0.000 0.000
#&gt; SRR1975475     3   0.257      0.914 0.000 0.012 0.852 0.136 0.000 0.000
#&gt; SRR1975476     3   0.257      0.914 0.000 0.012 0.852 0.136 0.000 0.000
#&gt; SRR1975473     5   0.385      0.522 0.000 0.456 0.000 0.000 0.544 0.000
#&gt; SRR1975474     5   0.385      0.522 0.000 0.456 0.000 0.000 0.544 0.000
#&gt; SRR1975471     1   0.000      0.888 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975472     1   0.000      0.888 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975469     1   0.405      0.762 0.792 0.000 0.040 0.000 0.068 0.100
#&gt; SRR1975470     1   0.405      0.762 0.792 0.000 0.040 0.000 0.068 0.100
#&gt; SRR1975467     3   0.236      0.811 0.000 0.136 0.860 0.000 0.000 0.004
#&gt; SRR1975468     3   0.236      0.811 0.000 0.136 0.860 0.000 0.000 0.004
#&gt; SRR1975465     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975466     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975463     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975464     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975461     5   0.441      0.419 0.232 0.000 0.076 0.000 0.692 0.000
#&gt; SRR1975462     5   0.441      0.419 0.232 0.000 0.076 0.000 0.692 0.000
#&gt; SRR1975459     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975460     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975457     5   0.385      0.522 0.000 0.456 0.000 0.000 0.544 0.000
#&gt; SRR1975458     5   0.385      0.522 0.000 0.456 0.000 0.000 0.544 0.000
#&gt; SRR1975455     5   0.385      0.522 0.000 0.456 0.000 0.000 0.544 0.000
#&gt; SRR1975456     5   0.385      0.522 0.000 0.456 0.000 0.000 0.544 0.000
#&gt; SRR1975453     5   0.454      0.394 0.256 0.000 0.076 0.000 0.668 0.000
#&gt; SRR1975454     5   0.454      0.394 0.256 0.000 0.076 0.000 0.668 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-5-a').click(function(){
  $('#tab-MAD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-hclust-signature_compare](figure_cola/MAD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-hclust-collect-classes](figure_cola/MAD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "kmeans"]
# you can also extract it by
# res = res_list["MAD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-kmeans-collect-plots](figure_cola/MAD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-kmeans-select-partition-number](figure_cola/MAD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.522           0.794       0.899         0.4807 0.514   0.514
#> 3 3 0.553           0.783       0.841         0.3708 0.751   0.543
#> 4 4 0.590           0.682       0.776         0.1118 0.932   0.797
#> 5 5 0.665           0.724       0.776         0.0620 0.922   0.735
#> 6 6 0.670           0.631       0.717         0.0401 0.984   0.935
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-kmeans-get-classes-1'>
<p><a id='tab-MAD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2   0.358      0.881 0.068 0.932
#&gt; SRR1975507     2   0.358      0.881 0.068 0.932
#&gt; SRR1975506     2   0.358      0.881 0.068 0.932
#&gt; SRR1975505     2   0.358      0.881 0.068 0.932
#&gt; SRR1975503     1   0.000      0.905 1.000 0.000
#&gt; SRR1975504     1   0.000      0.905 1.000 0.000
#&gt; SRR1975501     1   0.980      0.381 0.584 0.416
#&gt; SRR1975502     1   0.980      0.381 0.584 0.416
#&gt; SRR1975499     1   0.000      0.905 1.000 0.000
#&gt; SRR1975500     1   0.000      0.905 1.000 0.000
#&gt; SRR1975497     1   0.788      0.724 0.764 0.236
#&gt; SRR1975498     1   0.788      0.724 0.764 0.236
#&gt; SRR1975493     2   0.866      0.653 0.288 0.712
#&gt; SRR1975494     2   0.866      0.653 0.288 0.712
#&gt; SRR1975495     2   0.163      0.853 0.024 0.976
#&gt; SRR1975496     2   0.163      0.853 0.024 0.976
#&gt; SRR1975491     1   0.697      0.731 0.812 0.188
#&gt; SRR1975492     1   0.697      0.731 0.812 0.188
#&gt; SRR1975489     1   0.000      0.905 1.000 0.000
#&gt; SRR1975490     1   0.000      0.905 1.000 0.000
#&gt; SRR1975487     1   0.000      0.905 1.000 0.000
#&gt; SRR1975488     1   0.000      0.905 1.000 0.000
#&gt; SRR1975485     1   0.000      0.905 1.000 0.000
#&gt; SRR1975486     1   0.000      0.905 1.000 0.000
#&gt; SRR1975483     2   0.760      0.657 0.220 0.780
#&gt; SRR1975484     2   0.760      0.657 0.220 0.780
#&gt; SRR1975481     2   0.753      0.663 0.216 0.784
#&gt; SRR1975482     2   0.753      0.663 0.216 0.784
#&gt; SRR1975477     2   0.358      0.881 0.068 0.932
#&gt; SRR1975478     2   0.358      0.881 0.068 0.932
#&gt; SRR1975479     1   0.000      0.905 1.000 0.000
#&gt; SRR1975480     1   0.000      0.905 1.000 0.000
#&gt; SRR1975475     1   0.000      0.905 1.000 0.000
#&gt; SRR1975476     1   0.000      0.905 1.000 0.000
#&gt; SRR1975473     2   0.358      0.881 0.068 0.932
#&gt; SRR1975474     2   0.358      0.881 0.068 0.932
#&gt; SRR1975471     2   0.000      0.858 0.000 1.000
#&gt; SRR1975472     2   0.000      0.858 0.000 1.000
#&gt; SRR1975469     2   0.999     -0.103 0.484 0.516
#&gt; SRR1975470     2   0.999     -0.103 0.484 0.516
#&gt; SRR1975467     1   0.278      0.877 0.952 0.048
#&gt; SRR1975468     1   0.278      0.877 0.952 0.048
#&gt; SRR1975465     2   0.529      0.852 0.120 0.880
#&gt; SRR1975466     2   0.529      0.852 0.120 0.880
#&gt; SRR1975463     2   0.529      0.852 0.120 0.880
#&gt; SRR1975464     2   0.529      0.852 0.120 0.880
#&gt; SRR1975461     2   0.000      0.858 0.000 1.000
#&gt; SRR1975462     2   0.000      0.858 0.000 1.000
#&gt; SRR1975459     2   0.358      0.881 0.068 0.932
#&gt; SRR1975460     2   0.358      0.881 0.068 0.932
#&gt; SRR1975457     2   0.358      0.881 0.068 0.932
#&gt; SRR1975458     2   0.358      0.881 0.068 0.932
#&gt; SRR1975455     2   0.358      0.881 0.068 0.932
#&gt; SRR1975456     2   0.358      0.881 0.068 0.932
#&gt; SRR1975453     2   0.000      0.858 0.000 1.000
#&gt; SRR1975454     2   0.000      0.858 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-2'>
<p><a id='tab-MAD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     2   0.537      0.814 0.252 0.744 0.004
#&gt; SRR1975507     2   0.537      0.814 0.252 0.744 0.004
#&gt; SRR1975506     2   0.537      0.814 0.252 0.744 0.004
#&gt; SRR1975505     2   0.537      0.814 0.252 0.744 0.004
#&gt; SRR1975503     3   0.313      0.835 0.052 0.032 0.916
#&gt; SRR1975504     3   0.313      0.835 0.052 0.032 0.916
#&gt; SRR1975501     1   0.641      0.713 0.764 0.144 0.092
#&gt; SRR1975502     1   0.641      0.713 0.764 0.144 0.092
#&gt; SRR1975499     3   0.103      0.857 0.024 0.000 0.976
#&gt; SRR1975500     3   0.103      0.857 0.024 0.000 0.976
#&gt; SRR1975497     1   0.480      0.702 0.780 0.000 0.220
#&gt; SRR1975498     1   0.480      0.702 0.780 0.000 0.220
#&gt; SRR1975493     2   0.509      0.650 0.072 0.836 0.092
#&gt; SRR1975494     2   0.509      0.650 0.072 0.836 0.092
#&gt; SRR1975495     1   0.311      0.861 0.900 0.096 0.004
#&gt; SRR1975496     1   0.311      0.861 0.900 0.096 0.004
#&gt; SRR1975491     3   0.979      0.276 0.328 0.248 0.424
#&gt; SRR1975492     3   0.979      0.276 0.328 0.248 0.424
#&gt; SRR1975489     3   0.164      0.854 0.044 0.000 0.956
#&gt; SRR1975490     3   0.164      0.854 0.044 0.000 0.956
#&gt; SRR1975487     3   0.129      0.855 0.032 0.000 0.968
#&gt; SRR1975488     3   0.129      0.855 0.032 0.000 0.968
#&gt; SRR1975485     3   0.141      0.855 0.036 0.000 0.964
#&gt; SRR1975486     3   0.141      0.855 0.036 0.000 0.964
#&gt; SRR1975483     1   0.377      0.874 0.888 0.084 0.028
#&gt; SRR1975484     1   0.377      0.874 0.888 0.084 0.028
#&gt; SRR1975481     1   0.377      0.874 0.888 0.084 0.028
#&gt; SRR1975482     1   0.377      0.874 0.888 0.084 0.028
#&gt; SRR1975477     2   0.452      0.829 0.180 0.816 0.004
#&gt; SRR1975478     2   0.452      0.829 0.180 0.816 0.004
#&gt; SRR1975479     3   0.249      0.854 0.060 0.008 0.932
#&gt; SRR1975480     3   0.249      0.854 0.060 0.008 0.932
#&gt; SRR1975475     3   0.315      0.841 0.048 0.036 0.916
#&gt; SRR1975476     3   0.315      0.841 0.048 0.036 0.916
#&gt; SRR1975473     2   0.423      0.828 0.160 0.836 0.004
#&gt; SRR1975474     2   0.423      0.828 0.160 0.836 0.004
#&gt; SRR1975471     1   0.319      0.847 0.888 0.112 0.000
#&gt; SRR1975472     1   0.319      0.847 0.888 0.112 0.000
#&gt; SRR1975469     1   0.440      0.848 0.864 0.044 0.092
#&gt; SRR1975470     1   0.440      0.848 0.864 0.044 0.092
#&gt; SRR1975467     3   0.774      0.547 0.060 0.356 0.584
#&gt; SRR1975468     3   0.774      0.547 0.060 0.356 0.584
#&gt; SRR1975465     2   0.205      0.767 0.020 0.952 0.028
#&gt; SRR1975466     2   0.205      0.767 0.020 0.952 0.028
#&gt; SRR1975463     2   0.205      0.767 0.020 0.952 0.028
#&gt; SRR1975464     2   0.205      0.767 0.020 0.952 0.028
#&gt; SRR1975461     2   0.586      0.697 0.344 0.656 0.000
#&gt; SRR1975462     2   0.586      0.697 0.344 0.656 0.000
#&gt; SRR1975459     2   0.177      0.774 0.024 0.960 0.016
#&gt; SRR1975460     2   0.177      0.774 0.024 0.960 0.016
#&gt; SRR1975457     2   0.511      0.821 0.228 0.768 0.004
#&gt; SRR1975458     2   0.511      0.821 0.228 0.768 0.004
#&gt; SRR1975455     2   0.511      0.821 0.228 0.768 0.004
#&gt; SRR1975456     2   0.511      0.821 0.228 0.768 0.004
#&gt; SRR1975453     1   0.327      0.837 0.884 0.116 0.000
#&gt; SRR1975454     1   0.327      0.837 0.884 0.116 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-3'>
<p><a id='tab-MAD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.4336      0.651 0.060 0.128 0.812 0.000
#&gt; SRR1975507     3  0.4336      0.651 0.060 0.128 0.812 0.000
#&gt; SRR1975506     3  0.4336      0.651 0.060 0.128 0.812 0.000
#&gt; SRR1975505     3  0.4336      0.651 0.060 0.128 0.812 0.000
#&gt; SRR1975503     4  0.4175      0.805 0.012 0.212 0.000 0.776
#&gt; SRR1975504     4  0.4175      0.805 0.012 0.212 0.000 0.776
#&gt; SRR1975501     1  0.4063      0.768 0.808 0.172 0.004 0.016
#&gt; SRR1975502     1  0.4063      0.768 0.808 0.172 0.004 0.016
#&gt; SRR1975499     4  0.1913      0.874 0.020 0.040 0.000 0.940
#&gt; SRR1975500     4  0.1913      0.874 0.020 0.040 0.000 0.940
#&gt; SRR1975497     1  0.3711      0.790 0.864 0.076 0.008 0.052
#&gt; SRR1975498     1  0.3711      0.790 0.864 0.076 0.008 0.052
#&gt; SRR1975493     2  0.5334      0.339 0.004 0.588 0.400 0.008
#&gt; SRR1975494     2  0.5334      0.339 0.004 0.588 0.400 0.008
#&gt; SRR1975495     1  0.2973      0.868 0.884 0.020 0.096 0.000
#&gt; SRR1975496     1  0.2973      0.868 0.884 0.020 0.096 0.000
#&gt; SRR1975491     2  0.7741      0.580 0.224 0.592 0.060 0.124
#&gt; SRR1975492     2  0.7741      0.580 0.224 0.592 0.060 0.124
#&gt; SRR1975489     4  0.2131      0.871 0.032 0.036 0.000 0.932
#&gt; SRR1975490     4  0.2131      0.871 0.032 0.036 0.000 0.932
#&gt; SRR1975487     4  0.0672      0.876 0.008 0.008 0.000 0.984
#&gt; SRR1975488     4  0.0672      0.876 0.008 0.008 0.000 0.984
#&gt; SRR1975485     4  0.1411      0.873 0.020 0.020 0.000 0.960
#&gt; SRR1975486     4  0.1411      0.873 0.020 0.020 0.000 0.960
#&gt; SRR1975483     1  0.2675      0.870 0.892 0.008 0.100 0.000
#&gt; SRR1975484     1  0.2675      0.870 0.892 0.008 0.100 0.000
#&gt; SRR1975481     1  0.3934      0.865 0.836 0.048 0.116 0.000
#&gt; SRR1975482     1  0.3934      0.865 0.836 0.048 0.116 0.000
#&gt; SRR1975477     3  0.1398      0.676 0.004 0.040 0.956 0.000
#&gt; SRR1975478     3  0.1398      0.676 0.004 0.040 0.956 0.000
#&gt; SRR1975479     4  0.4578      0.839 0.052 0.160 0.000 0.788
#&gt; SRR1975480     4  0.4578      0.839 0.052 0.160 0.000 0.788
#&gt; SRR1975475     4  0.5102      0.789 0.048 0.220 0.000 0.732
#&gt; SRR1975476     4  0.5102      0.789 0.048 0.220 0.000 0.732
#&gt; SRR1975473     3  0.1743      0.669 0.004 0.056 0.940 0.000
#&gt; SRR1975474     3  0.1743      0.669 0.004 0.056 0.940 0.000
#&gt; SRR1975471     1  0.4638      0.826 0.788 0.060 0.152 0.000
#&gt; SRR1975472     1  0.4638      0.826 0.788 0.060 0.152 0.000
#&gt; SRR1975469     1  0.4226      0.844 0.836 0.084 0.072 0.008
#&gt; SRR1975470     1  0.4226      0.844 0.836 0.084 0.072 0.008
#&gt; SRR1975467     2  0.6768      0.624 0.004 0.620 0.148 0.228
#&gt; SRR1975468     2  0.6768      0.624 0.004 0.620 0.148 0.228
#&gt; SRR1975465     3  0.5105      0.149 0.004 0.432 0.564 0.000
#&gt; SRR1975466     3  0.5105      0.149 0.004 0.432 0.564 0.000
#&gt; SRR1975463     3  0.5105      0.149 0.004 0.432 0.564 0.000
#&gt; SRR1975464     3  0.5105      0.149 0.004 0.432 0.564 0.000
#&gt; SRR1975461     3  0.5938      0.551 0.136 0.168 0.696 0.000
#&gt; SRR1975462     3  0.5938      0.551 0.136 0.168 0.696 0.000
#&gt; SRR1975459     3  0.5080      0.178 0.004 0.420 0.576 0.000
#&gt; SRR1975460     3  0.5080      0.178 0.004 0.420 0.576 0.000
#&gt; SRR1975457     3  0.1109      0.690 0.028 0.004 0.968 0.000
#&gt; SRR1975458     3  0.1109      0.690 0.028 0.004 0.968 0.000
#&gt; SRR1975455     3  0.0921      0.690 0.028 0.000 0.972 0.000
#&gt; SRR1975456     3  0.0921      0.690 0.028 0.000 0.972 0.000
#&gt; SRR1975453     1  0.6049      0.733 0.680 0.120 0.200 0.000
#&gt; SRR1975454     1  0.6049      0.733 0.680 0.120 0.200 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-4'>
<p><a id='tab-MAD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR1975508     3  0.3727      0.721 0.020 0.016 0.812 0.000 NA
#&gt; SRR1975507     3  0.3727      0.721 0.020 0.016 0.812 0.000 NA
#&gt; SRR1975506     3  0.3727      0.721 0.020 0.016 0.812 0.000 NA
#&gt; SRR1975505     3  0.3727      0.721 0.020 0.016 0.812 0.000 NA
#&gt; SRR1975503     4  0.5283      0.755 0.000 0.188 0.000 0.676 NA
#&gt; SRR1975504     4  0.5283      0.755 0.000 0.188 0.000 0.676 NA
#&gt; SRR1975501     1  0.5033      0.714 0.716 0.124 0.000 0.004 NA
#&gt; SRR1975502     1  0.5033      0.714 0.716 0.124 0.000 0.004 NA
#&gt; SRR1975499     4  0.2616      0.836 0.000 0.036 0.000 0.888 NA
#&gt; SRR1975500     4  0.2616      0.836 0.000 0.036 0.000 0.888 NA
#&gt; SRR1975497     1  0.4906      0.722 0.704 0.016 0.004 0.032 NA
#&gt; SRR1975498     1  0.4906      0.722 0.704 0.016 0.004 0.032 NA
#&gt; SRR1975493     2  0.3243      0.685 0.004 0.812 0.180 0.000 NA
#&gt; SRR1975494     2  0.3243      0.685 0.004 0.812 0.180 0.000 NA
#&gt; SRR1975495     1  0.2876      0.824 0.888 0.016 0.044 0.000 NA
#&gt; SRR1975496     1  0.2876      0.824 0.888 0.016 0.044 0.000 NA
#&gt; SRR1975491     2  0.6229      0.397 0.156 0.648 0.004 0.036 NA
#&gt; SRR1975492     2  0.6229      0.397 0.156 0.648 0.004 0.036 NA
#&gt; SRR1975489     4  0.2477      0.838 0.008 0.008 0.000 0.892 NA
#&gt; SRR1975490     4  0.2477      0.838 0.008 0.008 0.000 0.892 NA
#&gt; SRR1975487     4  0.0727      0.843 0.004 0.004 0.000 0.980 NA
#&gt; SRR1975488     4  0.0727      0.843 0.004 0.004 0.000 0.980 NA
#&gt; SRR1975485     4  0.1731      0.842 0.012 0.008 0.000 0.940 NA
#&gt; SRR1975486     4  0.1731      0.842 0.012 0.008 0.000 0.940 NA
#&gt; SRR1975483     1  0.2104      0.827 0.924 0.008 0.044 0.000 NA
#&gt; SRR1975484     1  0.2104      0.827 0.924 0.008 0.044 0.000 NA
#&gt; SRR1975481     1  0.3634      0.819 0.844 0.020 0.056 0.000 NA
#&gt; SRR1975482     1  0.3634      0.819 0.844 0.020 0.056 0.000 NA
#&gt; SRR1975477     3  0.3446      0.716 0.016 0.112 0.844 0.000 NA
#&gt; SRR1975478     3  0.3446      0.716 0.016 0.112 0.844 0.000 NA
#&gt; SRR1975479     4  0.5293      0.789 0.016 0.044 0.008 0.680 NA
#&gt; SRR1975480     4  0.5293      0.789 0.016 0.044 0.008 0.680 NA
#&gt; SRR1975475     4  0.6425      0.733 0.008 0.160 0.008 0.576 NA
#&gt; SRR1975476     4  0.6425      0.733 0.008 0.160 0.008 0.576 NA
#&gt; SRR1975473     3  0.3846      0.690 0.016 0.132 0.816 0.000 NA
#&gt; SRR1975474     3  0.3846      0.690 0.016 0.132 0.816 0.000 NA
#&gt; SRR1975471     1  0.4499      0.758 0.764 0.004 0.096 0.000 NA
#&gt; SRR1975472     1  0.4499      0.758 0.764 0.004 0.096 0.000 NA
#&gt; SRR1975469     1  0.4245      0.795 0.788 0.024 0.036 0.000 NA
#&gt; SRR1975470     1  0.4245      0.795 0.788 0.024 0.036 0.000 NA
#&gt; SRR1975467     2  0.4360      0.578 0.004 0.804 0.028 0.104 NA
#&gt; SRR1975468     2  0.4360      0.578 0.004 0.804 0.028 0.104 NA
#&gt; SRR1975465     2  0.4671      0.668 0.000 0.640 0.332 0.000 NA
#&gt; SRR1975466     2  0.4671      0.668 0.000 0.640 0.332 0.000 NA
#&gt; SRR1975463     2  0.4592      0.669 0.000 0.644 0.332 0.000 NA
#&gt; SRR1975464     2  0.4592      0.669 0.000 0.644 0.332 0.000 NA
#&gt; SRR1975461     3  0.6090      0.531 0.144 0.008 0.588 0.000 NA
#&gt; SRR1975462     3  0.6090      0.531 0.144 0.008 0.588 0.000 NA
#&gt; SRR1975459     2  0.4733      0.645 0.000 0.624 0.348 0.000 NA
#&gt; SRR1975460     2  0.4733      0.645 0.000 0.624 0.348 0.000 NA
#&gt; SRR1975457     3  0.1914      0.760 0.016 0.060 0.924 0.000 NA
#&gt; SRR1975458     3  0.1914      0.760 0.016 0.060 0.924 0.000 NA
#&gt; SRR1975455     3  0.2199      0.759 0.016 0.060 0.916 0.000 NA
#&gt; SRR1975456     3  0.2199      0.759 0.016 0.060 0.916 0.000 NA
#&gt; SRR1975453     1  0.5852      0.633 0.624 0.004 0.180 0.000 NA
#&gt; SRR1975454     1  0.5852      0.633 0.624 0.004 0.180 0.000 NA
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-5'>
<p><a id='tab-MAD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     5  0.4543      0.191 0.004 0.008 0.292 0.000 0.660 0.036
#&gt; SRR1975507     5  0.4543      0.191 0.004 0.008 0.292 0.000 0.660 0.036
#&gt; SRR1975506     5  0.4543      0.191 0.004 0.008 0.292 0.000 0.660 0.036
#&gt; SRR1975505     5  0.4543      0.191 0.004 0.008 0.292 0.000 0.660 0.036
#&gt; SRR1975503     4  0.6047      0.665 0.000 0.128 0.032 0.508 0.000 0.332
#&gt; SRR1975504     4  0.6047      0.665 0.000 0.128 0.032 0.508 0.000 0.332
#&gt; SRR1975501     1  0.5250      0.648 0.676 0.052 0.204 0.004 0.000 0.064
#&gt; SRR1975502     1  0.5250      0.648 0.676 0.052 0.204 0.004 0.000 0.064
#&gt; SRR1975499     4  0.4334      0.744 0.000 0.028 0.028 0.716 0.000 0.228
#&gt; SRR1975500     4  0.4334      0.744 0.000 0.028 0.028 0.716 0.000 0.228
#&gt; SRR1975497     1  0.5286      0.643 0.648 0.016 0.256 0.024 0.000 0.056
#&gt; SRR1975498     1  0.5286      0.643 0.648 0.016 0.256 0.024 0.000 0.056
#&gt; SRR1975493     2  0.4210      0.667 0.000 0.748 0.008 0.000 0.164 0.080
#&gt; SRR1975494     2  0.4210      0.667 0.000 0.748 0.008 0.000 0.164 0.080
#&gt; SRR1975495     1  0.2482      0.730 0.892 0.004 0.072 0.000 0.020 0.012
#&gt; SRR1975496     1  0.2482      0.730 0.892 0.004 0.072 0.000 0.020 0.012
#&gt; SRR1975491     2  0.7209      0.335 0.120 0.488 0.112 0.012 0.008 0.260
#&gt; SRR1975492     2  0.7209      0.335 0.120 0.488 0.112 0.012 0.008 0.260
#&gt; SRR1975489     4  0.2006      0.763 0.000 0.000 0.016 0.904 0.000 0.080
#&gt; SRR1975490     4  0.2006      0.763 0.000 0.000 0.016 0.904 0.000 0.080
#&gt; SRR1975487     4  0.2230      0.766 0.000 0.000 0.024 0.892 0.000 0.084
#&gt; SRR1975488     4  0.2230      0.766 0.000 0.000 0.024 0.892 0.000 0.084
#&gt; SRR1975485     4  0.1401      0.766 0.004 0.000 0.020 0.948 0.000 0.028
#&gt; SRR1975486     4  0.1401      0.766 0.004 0.000 0.020 0.948 0.000 0.028
#&gt; SRR1975483     1  0.2255      0.736 0.912 0.004 0.036 0.000 0.020 0.028
#&gt; SRR1975484     1  0.2255      0.736 0.912 0.004 0.036 0.000 0.020 0.028
#&gt; SRR1975481     1  0.3774      0.720 0.824 0.016 0.072 0.000 0.020 0.068
#&gt; SRR1975482     1  0.3774      0.720 0.824 0.016 0.072 0.000 0.020 0.068
#&gt; SRR1975477     5  0.2065      0.683 0.004 0.056 0.012 0.000 0.916 0.012
#&gt; SRR1975478     5  0.2065      0.683 0.004 0.056 0.012 0.000 0.916 0.012
#&gt; SRR1975479     4  0.5633      0.692 0.004 0.056 0.040 0.588 0.004 0.308
#&gt; SRR1975480     4  0.5633      0.692 0.004 0.056 0.040 0.588 0.004 0.308
#&gt; SRR1975475     4  0.6009      0.625 0.004 0.132 0.008 0.440 0.004 0.412
#&gt; SRR1975476     4  0.6009      0.625 0.004 0.132 0.008 0.440 0.004 0.412
#&gt; SRR1975473     5  0.2990      0.653 0.008 0.076 0.020 0.000 0.868 0.028
#&gt; SRR1975474     5  0.2990      0.653 0.008 0.076 0.020 0.000 0.868 0.028
#&gt; SRR1975471     1  0.4028      0.604 0.752 0.000 0.192 0.000 0.044 0.012
#&gt; SRR1975472     1  0.4028      0.604 0.752 0.000 0.192 0.000 0.044 0.012
#&gt; SRR1975469     1  0.4964      0.692 0.732 0.028 0.092 0.000 0.020 0.128
#&gt; SRR1975470     1  0.4964      0.692 0.732 0.028 0.092 0.000 0.020 0.128
#&gt; SRR1975467     2  0.4882      0.516 0.000 0.712 0.024 0.048 0.020 0.196
#&gt; SRR1975468     2  0.4882      0.516 0.000 0.712 0.024 0.048 0.020 0.196
#&gt; SRR1975465     2  0.3584      0.664 0.000 0.688 0.004 0.000 0.308 0.000
#&gt; SRR1975466     2  0.3584      0.664 0.000 0.688 0.004 0.000 0.308 0.000
#&gt; SRR1975463     2  0.3707      0.662 0.000 0.680 0.008 0.000 0.312 0.000
#&gt; SRR1975464     2  0.3707      0.662 0.000 0.680 0.008 0.000 0.312 0.000
#&gt; SRR1975461     3  0.5983      1.000 0.156 0.012 0.432 0.000 0.400 0.000
#&gt; SRR1975462     3  0.5983      1.000 0.156 0.012 0.432 0.000 0.400 0.000
#&gt; SRR1975459     2  0.3725      0.657 0.000 0.676 0.008 0.000 0.316 0.000
#&gt; SRR1975460     2  0.3725      0.657 0.000 0.676 0.008 0.000 0.316 0.000
#&gt; SRR1975457     5  0.1312      0.690 0.008 0.004 0.020 0.000 0.956 0.012
#&gt; SRR1975458     5  0.1312      0.690 0.008 0.004 0.020 0.000 0.956 0.012
#&gt; SRR1975455     5  0.0767      0.696 0.008 0.004 0.012 0.000 0.976 0.000
#&gt; SRR1975456     5  0.0767      0.696 0.008 0.004 0.012 0.000 0.976 0.000
#&gt; SRR1975453     1  0.5296      0.267 0.568 0.000 0.336 0.000 0.084 0.012
#&gt; SRR1975454     1  0.5296      0.267 0.568 0.000 0.336 0.000 0.084 0.012
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-kmeans-signature_compare](figure_cola/MAD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-kmeans-collect-classes](figure_cola/MAD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "skmeans"]
# you can also extract it by
# res = res_list["MAD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-skmeans-collect-plots](figure_cola/MAD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-skmeans-select-partition-number](figure_cola/MAD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.860           0.861       0.943         0.5084 0.491   0.491
#> 3 3 1.000           0.981       0.991         0.3253 0.758   0.544
#> 4 4 1.000           0.975       0.978         0.1274 0.870   0.627
#> 5 5 0.849           0.771       0.872         0.0577 0.909   0.650
#> 6 6 0.849           0.697       0.834         0.0323 0.953   0.778
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 3
```

There is also optional best $k$ = 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-skmeans-get-classes-1'>
<p><a id='tab-MAD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975507     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975506     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975505     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975503     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975504     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975501     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975502     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975499     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975500     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975497     1  0.3431      0.879 0.936 0.064
#&gt; SRR1975498     1  0.3431      0.879 0.936 0.064
#&gt; SRR1975493     2  0.9866      0.262 0.432 0.568
#&gt; SRR1975494     2  0.9866      0.262 0.432 0.568
#&gt; SRR1975495     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975496     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975491     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975492     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975489     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975490     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975487     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975488     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975485     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975486     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975483     1  0.9909      0.307 0.556 0.444
#&gt; SRR1975484     1  0.9909      0.307 0.556 0.444
#&gt; SRR1975481     1  0.9922      0.296 0.552 0.448
#&gt; SRR1975482     1  0.9922      0.296 0.552 0.448
#&gt; SRR1975477     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975478     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975479     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975480     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975475     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975476     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975473     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975474     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975471     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975472     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975469     1  0.3431      0.879 0.936 0.064
#&gt; SRR1975470     1  0.3431      0.879 0.936 0.064
#&gt; SRR1975467     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975468     1  0.0000      0.919 1.000 0.000
#&gt; SRR1975465     2  0.3431      0.906 0.064 0.936
#&gt; SRR1975466     2  0.3431      0.906 0.064 0.936
#&gt; SRR1975463     2  0.3431      0.906 0.064 0.936
#&gt; SRR1975464     2  0.3431      0.906 0.064 0.936
#&gt; SRR1975461     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975462     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975459     2  0.0938      0.946 0.012 0.988
#&gt; SRR1975460     2  0.0938      0.946 0.012 0.988
#&gt; SRR1975457     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975458     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975455     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975456     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975453     2  0.0000      0.953 0.000 1.000
#&gt; SRR1975454     2  0.0000      0.953 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-2'>
<p><a id='tab-MAD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975507     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975506     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975505     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975503     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975504     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975501     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975502     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975499     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975500     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975497     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975493     2  0.4605      0.757 0.000 0.796 0.204
#&gt; SRR1975494     2  0.4605      0.757 0.000 0.796 0.204
#&gt; SRR1975495     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975491     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975492     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975489     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975490     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975487     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975488     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975485     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975486     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975483     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975477     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975478     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975479     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975480     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975475     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975476     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975473     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975474     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975471     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975469     1  0.0424      0.992 0.992 0.000 0.008
#&gt; SRR1975470     1  0.0424      0.992 0.992 0.000 0.008
#&gt; SRR1975467     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975468     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975465     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975466     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975463     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975464     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975461     2  0.1411      0.948 0.036 0.964 0.000
#&gt; SRR1975462     2  0.1411      0.948 0.036 0.964 0.000
#&gt; SRR1975459     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975460     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975457     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975458     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975455     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975456     2  0.0000      0.976 0.000 1.000 0.000
#&gt; SRR1975453     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1975454     1  0.0000      0.999 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-3'>
<p><a id='tab-MAD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.0000      0.982 0.000 0.000 1.000 0.000
#&gt; SRR1975507     3  0.0000      0.982 0.000 0.000 1.000 0.000
#&gt; SRR1975506     3  0.0000      0.982 0.000 0.000 1.000 0.000
#&gt; SRR1975505     3  0.0000      0.982 0.000 0.000 1.000 0.000
#&gt; SRR1975503     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975504     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975501     1  0.0707      0.981 0.980 0.020 0.000 0.000
#&gt; SRR1975502     1  0.0707      0.981 0.980 0.020 0.000 0.000
#&gt; SRR1975499     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975500     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975497     1  0.0927      0.980 0.976 0.016 0.000 0.008
#&gt; SRR1975498     1  0.0927      0.980 0.976 0.016 0.000 0.008
#&gt; SRR1975493     2  0.0817      0.953 0.000 0.976 0.024 0.000
#&gt; SRR1975494     2  0.0817      0.953 0.000 0.976 0.024 0.000
#&gt; SRR1975495     1  0.0336      0.981 0.992 0.008 0.000 0.000
#&gt; SRR1975496     1  0.0336      0.981 0.992 0.008 0.000 0.000
#&gt; SRR1975491     2  0.3342      0.875 0.032 0.868 0.000 0.100
#&gt; SRR1975492     2  0.3342      0.875 0.032 0.868 0.000 0.100
#&gt; SRR1975489     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975487     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975488     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975485     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975486     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975483     1  0.0000      0.983 1.000 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.983 1.000 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0469      0.983 0.988 0.012 0.000 0.000
#&gt; SRR1975482     1  0.0469      0.983 0.988 0.012 0.000 0.000
#&gt; SRR1975477     3  0.0921      0.981 0.000 0.028 0.972 0.000
#&gt; SRR1975478     3  0.0921      0.981 0.000 0.028 0.972 0.000
#&gt; SRR1975479     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975480     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975475     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975476     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1975473     3  0.0921      0.981 0.000 0.028 0.972 0.000
#&gt; SRR1975474     3  0.0921      0.981 0.000 0.028 0.972 0.000
#&gt; SRR1975471     1  0.1042      0.973 0.972 0.008 0.020 0.000
#&gt; SRR1975472     1  0.1042      0.973 0.972 0.008 0.020 0.000
#&gt; SRR1975469     1  0.0779      0.982 0.980 0.016 0.000 0.004
#&gt; SRR1975470     1  0.0779      0.982 0.980 0.016 0.000 0.004
#&gt; SRR1975467     2  0.1792      0.923 0.000 0.932 0.000 0.068
#&gt; SRR1975468     2  0.1792      0.923 0.000 0.932 0.000 0.068
#&gt; SRR1975465     2  0.1211      0.955 0.000 0.960 0.040 0.000
#&gt; SRR1975466     2  0.1211      0.955 0.000 0.960 0.040 0.000
#&gt; SRR1975463     2  0.1211      0.955 0.000 0.960 0.040 0.000
#&gt; SRR1975464     2  0.1211      0.955 0.000 0.960 0.040 0.000
#&gt; SRR1975461     3  0.0927      0.965 0.016 0.008 0.976 0.000
#&gt; SRR1975462     3  0.0927      0.965 0.016 0.008 0.976 0.000
#&gt; SRR1975459     2  0.1211      0.955 0.000 0.960 0.040 0.000
#&gt; SRR1975460     2  0.1211      0.955 0.000 0.960 0.040 0.000
#&gt; SRR1975457     3  0.0592      0.985 0.000 0.016 0.984 0.000
#&gt; SRR1975458     3  0.0592      0.985 0.000 0.016 0.984 0.000
#&gt; SRR1975455     3  0.0592      0.985 0.000 0.016 0.984 0.000
#&gt; SRR1975456     3  0.0592      0.985 0.000 0.016 0.984 0.000
#&gt; SRR1975453     1  0.1452      0.963 0.956 0.008 0.036 0.000
#&gt; SRR1975454     1  0.1452      0.963 0.956 0.008 0.036 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-4'>
<p><a id='tab-MAD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.3586      0.768 0.000 0.000 0.736 0.000 0.264
#&gt; SRR1975507     3  0.3586      0.768 0.000 0.000 0.736 0.000 0.264
#&gt; SRR1975506     3  0.3586      0.768 0.000 0.000 0.736 0.000 0.264
#&gt; SRR1975505     3  0.3586      0.768 0.000 0.000 0.736 0.000 0.264
#&gt; SRR1975503     4  0.0609      0.983 0.020 0.000 0.000 0.980 0.000
#&gt; SRR1975504     4  0.0609      0.983 0.020 0.000 0.000 0.980 0.000
#&gt; SRR1975501     1  0.1851      0.676 0.912 0.000 0.000 0.000 0.088
#&gt; SRR1975502     1  0.1851      0.676 0.912 0.000 0.000 0.000 0.088
#&gt; SRR1975499     4  0.0000      0.996 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975500     4  0.0000      0.996 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975497     1  0.2338      0.684 0.884 0.000 0.000 0.004 0.112
#&gt; SRR1975498     1  0.2338      0.684 0.884 0.000 0.000 0.004 0.112
#&gt; SRR1975493     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975494     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975495     5  0.3774      0.489 0.296 0.000 0.000 0.000 0.704
#&gt; SRR1975496     5  0.3774      0.489 0.296 0.000 0.000 0.000 0.704
#&gt; SRR1975491     1  0.4988      0.328 0.656 0.284 0.000 0.060 0.000
#&gt; SRR1975492     1  0.4988      0.328 0.656 0.284 0.000 0.060 0.000
#&gt; SRR1975489     4  0.0000      0.996 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975490     4  0.0000      0.996 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975487     4  0.0000      0.996 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975488     4  0.0000      0.996 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975485     4  0.0000      0.996 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975486     4  0.0000      0.996 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975483     5  0.4249      0.222 0.432 0.000 0.000 0.000 0.568
#&gt; SRR1975484     5  0.4249      0.222 0.432 0.000 0.000 0.000 0.568
#&gt; SRR1975481     1  0.4201      0.222 0.592 0.000 0.000 0.000 0.408
#&gt; SRR1975482     1  0.4201      0.222 0.592 0.000 0.000 0.000 0.408
#&gt; SRR1975477     3  0.0162      0.896 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975478     3  0.0162      0.896 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975479     4  0.0000      0.996 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975480     4  0.0000      0.996 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975475     4  0.0324      0.992 0.004 0.000 0.000 0.992 0.004
#&gt; SRR1975476     4  0.0324      0.992 0.004 0.000 0.000 0.992 0.004
#&gt; SRR1975473     3  0.0290      0.894 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1975474     3  0.0290      0.894 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1975471     5  0.2605      0.605 0.148 0.000 0.000 0.000 0.852
#&gt; SRR1975472     5  0.2605      0.605 0.148 0.000 0.000 0.000 0.852
#&gt; SRR1975469     1  0.3086      0.646 0.816 0.000 0.000 0.004 0.180
#&gt; SRR1975470     1  0.3086      0.646 0.816 0.000 0.000 0.004 0.180
#&gt; SRR1975467     2  0.2585      0.903 0.064 0.896 0.000 0.036 0.004
#&gt; SRR1975468     2  0.2585      0.903 0.064 0.896 0.000 0.036 0.004
#&gt; SRR1975465     2  0.0510      0.972 0.000 0.984 0.016 0.000 0.000
#&gt; SRR1975466     2  0.0510      0.972 0.000 0.984 0.016 0.000 0.000
#&gt; SRR1975463     2  0.0510      0.972 0.000 0.984 0.016 0.000 0.000
#&gt; SRR1975464     2  0.0510      0.972 0.000 0.984 0.016 0.000 0.000
#&gt; SRR1975461     5  0.3707      0.266 0.000 0.000 0.284 0.000 0.716
#&gt; SRR1975462     5  0.3707      0.266 0.000 0.000 0.284 0.000 0.716
#&gt; SRR1975459     2  0.0510      0.972 0.000 0.984 0.016 0.000 0.000
#&gt; SRR1975460     2  0.0510      0.972 0.000 0.984 0.016 0.000 0.000
#&gt; SRR1975457     3  0.0324      0.896 0.000 0.004 0.992 0.000 0.004
#&gt; SRR1975458     3  0.0324      0.896 0.000 0.004 0.992 0.000 0.004
#&gt; SRR1975455     3  0.0162      0.896 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975456     3  0.0162      0.896 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975453     5  0.0324      0.594 0.004 0.000 0.004 0.000 0.992
#&gt; SRR1975454     5  0.0324      0.594 0.004 0.000 0.004 0.000 0.992
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-5'>
<p><a id='tab-MAD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     5  0.4460     0.4846 0.000 0.000 0.452 0.000 0.520 0.028
#&gt; SRR1975507     5  0.4460     0.4846 0.000 0.000 0.452 0.000 0.520 0.028
#&gt; SRR1975506     5  0.4460     0.4846 0.000 0.000 0.452 0.000 0.520 0.028
#&gt; SRR1975505     5  0.4460     0.4846 0.000 0.000 0.452 0.000 0.520 0.028
#&gt; SRR1975503     4  0.2658     0.8666 0.000 0.008 0.016 0.864 0.000 0.112
#&gt; SRR1975504     4  0.2658     0.8666 0.000 0.008 0.016 0.864 0.000 0.112
#&gt; SRR1975501     1  0.4407     0.0513 0.492 0.000 0.024 0.000 0.000 0.484
#&gt; SRR1975502     1  0.4407     0.0513 0.492 0.000 0.024 0.000 0.000 0.484
#&gt; SRR1975499     4  0.0291     0.9571 0.000 0.000 0.004 0.992 0.000 0.004
#&gt; SRR1975500     4  0.0291     0.9571 0.000 0.000 0.004 0.992 0.000 0.004
#&gt; SRR1975497     1  0.3767     0.4237 0.708 0.000 0.012 0.004 0.000 0.276
#&gt; SRR1975498     1  0.3767     0.4237 0.708 0.000 0.012 0.004 0.000 0.276
#&gt; SRR1975493     2  0.1124     0.8878 0.000 0.956 0.000 0.000 0.008 0.036
#&gt; SRR1975494     2  0.1124     0.8878 0.000 0.956 0.000 0.000 0.008 0.036
#&gt; SRR1975495     1  0.4084     0.1113 0.588 0.000 0.400 0.000 0.000 0.012
#&gt; SRR1975496     1  0.4084     0.1113 0.588 0.000 0.400 0.000 0.000 0.012
#&gt; SRR1975491     6  0.2401     1.0000 0.044 0.036 0.000 0.020 0.000 0.900
#&gt; SRR1975492     6  0.2401     1.0000 0.044 0.036 0.000 0.020 0.000 0.900
#&gt; SRR1975489     4  0.0146     0.9572 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975490     4  0.0146     0.9572 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975487     4  0.0146     0.9573 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975488     4  0.0146     0.9573 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975485     4  0.0146     0.9573 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975486     4  0.0146     0.9573 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1975483     1  0.2969     0.4599 0.776 0.000 0.224 0.000 0.000 0.000
#&gt; SRR1975484     1  0.2969     0.4599 0.776 0.000 0.224 0.000 0.000 0.000
#&gt; SRR1975481     1  0.3413     0.5514 0.812 0.000 0.108 0.000 0.000 0.080
#&gt; SRR1975482     1  0.3413     0.5514 0.812 0.000 0.108 0.000 0.000 0.080
#&gt; SRR1975477     5  0.0508     0.7938 0.000 0.004 0.000 0.000 0.984 0.012
#&gt; SRR1975478     5  0.0508     0.7938 0.000 0.004 0.000 0.000 0.984 0.012
#&gt; SRR1975479     4  0.1562     0.9383 0.004 0.000 0.024 0.940 0.000 0.032
#&gt; SRR1975480     4  0.1562     0.9383 0.004 0.000 0.024 0.940 0.000 0.032
#&gt; SRR1975475     4  0.2022     0.9305 0.000 0.008 0.024 0.916 0.000 0.052
#&gt; SRR1975476     4  0.2022     0.9305 0.000 0.008 0.024 0.916 0.000 0.052
#&gt; SRR1975473     5  0.0767     0.7900 0.000 0.004 0.008 0.000 0.976 0.012
#&gt; SRR1975474     5  0.0767     0.7900 0.000 0.004 0.008 0.000 0.976 0.012
#&gt; SRR1975471     3  0.3907     0.3487 0.408 0.000 0.588 0.000 0.000 0.004
#&gt; SRR1975472     3  0.3907     0.3487 0.408 0.000 0.588 0.000 0.000 0.004
#&gt; SRR1975469     1  0.3250     0.5170 0.788 0.000 0.012 0.004 0.000 0.196
#&gt; SRR1975470     1  0.3250     0.5170 0.788 0.000 0.012 0.004 0.000 0.196
#&gt; SRR1975467     2  0.4498     0.5298 0.000 0.640 0.016 0.024 0.000 0.320
#&gt; SRR1975468     2  0.4498     0.5298 0.000 0.640 0.016 0.024 0.000 0.320
#&gt; SRR1975465     2  0.0363     0.9030 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1975466     2  0.0363     0.9030 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1975463     2  0.0363     0.9030 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1975464     2  0.0363     0.9030 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1975461     3  0.2312     0.5577 0.000 0.000 0.876 0.000 0.112 0.012
#&gt; SRR1975462     3  0.2312     0.5577 0.000 0.000 0.876 0.000 0.112 0.012
#&gt; SRR1975459     2  0.0363     0.9030 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1975460     2  0.0363     0.9030 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1975457     5  0.0458     0.7981 0.000 0.000 0.016 0.000 0.984 0.000
#&gt; SRR1975458     5  0.0458     0.7981 0.000 0.000 0.016 0.000 0.984 0.000
#&gt; SRR1975455     5  0.0260     0.7984 0.000 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1975456     5  0.0260     0.7984 0.000 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1975453     3  0.2703     0.6555 0.172 0.000 0.824 0.000 0.000 0.004
#&gt; SRR1975454     3  0.2703     0.6555 0.172 0.000 0.824 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-skmeans-signature_compare](figure_cola/MAD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-skmeans-collect-classes](figure_cola/MAD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "pam"]
# you can also extract it by
# res = res_list["MAD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-pam-collect-plots](figure_cola/MAD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-pam-select-partition-number](figure_cola/MAD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.675           0.916       0.951         0.4575 0.514   0.514
#> 3 3 0.797           0.715       0.888         0.4508 0.579   0.339
#> 4 4 0.983           0.945       0.977         0.1469 0.823   0.531
#> 5 5 0.975           0.942       0.972         0.0445 0.927   0.717
#> 6 6 0.897           0.852       0.910         0.0362 0.990   0.949
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 4
```

There is also optional best $k$ = 4 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-classes'>
<ul>
<li><a href='#tab-MAD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-pam-get-classes-1'>
<p><a id='tab-MAD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2   0.000      0.993 0.000 1.000
#&gt; SRR1975507     2   0.000      0.993 0.000 1.000
#&gt; SRR1975506     2   0.000      0.993 0.000 1.000
#&gt; SRR1975505     2   0.000      0.993 0.000 1.000
#&gt; SRR1975503     1   0.000      0.873 1.000 0.000
#&gt; SRR1975504     1   0.000      0.873 1.000 0.000
#&gt; SRR1975501     1   0.795      0.751 0.760 0.240
#&gt; SRR1975502     1   0.802      0.747 0.756 0.244
#&gt; SRR1975499     1   0.000      0.873 1.000 0.000
#&gt; SRR1975500     1   0.000      0.873 1.000 0.000
#&gt; SRR1975497     1   0.506      0.846 0.888 0.112
#&gt; SRR1975498     1   0.625      0.823 0.844 0.156
#&gt; SRR1975493     2   0.443      0.883 0.092 0.908
#&gt; SRR1975494     2   0.443      0.883 0.092 0.908
#&gt; SRR1975495     2   0.000      0.993 0.000 1.000
#&gt; SRR1975496     2   0.000      0.993 0.000 1.000
#&gt; SRR1975491     1   0.939      0.609 0.644 0.356
#&gt; SRR1975492     1   0.939      0.609 0.644 0.356
#&gt; SRR1975489     1   0.000      0.873 1.000 0.000
#&gt; SRR1975490     1   0.000      0.873 1.000 0.000
#&gt; SRR1975487     1   0.000      0.873 1.000 0.000
#&gt; SRR1975488     1   0.000      0.873 1.000 0.000
#&gt; SRR1975485     1   0.000      0.873 1.000 0.000
#&gt; SRR1975486     1   0.000      0.873 1.000 0.000
#&gt; SRR1975483     2   0.000      0.993 0.000 1.000
#&gt; SRR1975484     2   0.000      0.993 0.000 1.000
#&gt; SRR1975481     2   0.000      0.993 0.000 1.000
#&gt; SRR1975482     2   0.000      0.993 0.000 1.000
#&gt; SRR1975477     2   0.000      0.993 0.000 1.000
#&gt; SRR1975478     2   0.000      0.993 0.000 1.000
#&gt; SRR1975479     1   0.295      0.863 0.948 0.052
#&gt; SRR1975480     1   0.295      0.863 0.948 0.052
#&gt; SRR1975475     1   0.574      0.831 0.864 0.136
#&gt; SRR1975476     1   0.563      0.833 0.868 0.132
#&gt; SRR1975473     2   0.000      0.993 0.000 1.000
#&gt; SRR1975474     2   0.000      0.993 0.000 1.000
#&gt; SRR1975471     2   0.000      0.993 0.000 1.000
#&gt; SRR1975472     2   0.000      0.993 0.000 1.000
#&gt; SRR1975469     2   0.000      0.993 0.000 1.000
#&gt; SRR1975470     2   0.000      0.993 0.000 1.000
#&gt; SRR1975467     1   0.939      0.609 0.644 0.356
#&gt; SRR1975468     1   0.939      0.609 0.644 0.356
#&gt; SRR1975465     2   0.000      0.993 0.000 1.000
#&gt; SRR1975466     2   0.000      0.993 0.000 1.000
#&gt; SRR1975463     2   0.000      0.993 0.000 1.000
#&gt; SRR1975464     2   0.000      0.993 0.000 1.000
#&gt; SRR1975461     2   0.000      0.993 0.000 1.000
#&gt; SRR1975462     2   0.000      0.993 0.000 1.000
#&gt; SRR1975459     2   0.000      0.993 0.000 1.000
#&gt; SRR1975460     2   0.000      0.993 0.000 1.000
#&gt; SRR1975457     2   0.000      0.993 0.000 1.000
#&gt; SRR1975458     2   0.000      0.993 0.000 1.000
#&gt; SRR1975455     2   0.000      0.993 0.000 1.000
#&gt; SRR1975456     2   0.000      0.993 0.000 1.000
#&gt; SRR1975453     2   0.000      0.993 0.000 1.000
#&gt; SRR1975454     2   0.000      0.993 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-1-a').click(function(){
  $('#tab-MAD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-2'>
<p><a id='tab-MAD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     2  0.6936      0.785 0.016 0.524 0.460
#&gt; SRR1975507     2  0.7838      0.756 0.052 0.488 0.460
#&gt; SRR1975506     2  0.8210      0.736 0.072 0.468 0.460
#&gt; SRR1975505     2  0.7283      0.777 0.028 0.512 0.460
#&gt; SRR1975503     3  0.6280      0.796 0.000 0.460 0.540
#&gt; SRR1975504     3  0.6280      0.796 0.000 0.460 0.540
#&gt; SRR1975501     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975502     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975499     3  0.6280      0.796 0.000 0.460 0.540
#&gt; SRR1975500     3  0.6280      0.796 0.000 0.460 0.540
#&gt; SRR1975497     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975493     2  0.5785      0.707 0.000 0.668 0.332
#&gt; SRR1975494     2  0.5785      0.707 0.000 0.668 0.332
#&gt; SRR1975495     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975491     2  0.6772     -0.264 0.304 0.664 0.032
#&gt; SRR1975492     2  0.6448     -0.255 0.328 0.656 0.016
#&gt; SRR1975489     3  0.6280      0.796 0.000 0.460 0.540
#&gt; SRR1975490     3  0.6280      0.796 0.000 0.460 0.540
#&gt; SRR1975487     3  0.6280      0.796 0.000 0.460 0.540
#&gt; SRR1975488     3  0.6280      0.796 0.000 0.460 0.540
#&gt; SRR1975485     3  0.6280      0.796 0.000 0.460 0.540
#&gt; SRR1975486     3  0.6280      0.796 0.000 0.460 0.540
#&gt; SRR1975483     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975477     2  0.6280      0.792 0.000 0.540 0.460
#&gt; SRR1975478     2  0.6280      0.792 0.000 0.540 0.460
#&gt; SRR1975479     3  0.6192      0.616 0.000 0.420 0.580
#&gt; SRR1975480     3  0.6154      0.640 0.000 0.408 0.592
#&gt; SRR1975475     2  0.0237      0.251 0.000 0.996 0.004
#&gt; SRR1975476     2  0.0237      0.237 0.000 0.996 0.004
#&gt; SRR1975473     2  0.6280      0.792 0.000 0.540 0.460
#&gt; SRR1975474     2  0.6280      0.792 0.000 0.540 0.460
#&gt; SRR1975471     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975469     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975470     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975467     2  0.0237      0.236 0.000 0.996 0.004
#&gt; SRR1975468     2  0.0237      0.236 0.000 0.996 0.004
#&gt; SRR1975465     2  0.6280      0.792 0.000 0.540 0.460
#&gt; SRR1975466     2  0.6280      0.792 0.000 0.540 0.460
#&gt; SRR1975463     2  0.6280      0.792 0.000 0.540 0.460
#&gt; SRR1975464     2  0.6280      0.792 0.000 0.540 0.460
#&gt; SRR1975461     1  0.0892      0.979 0.980 0.000 0.020
#&gt; SRR1975462     1  0.0892      0.979 0.980 0.000 0.020
#&gt; SRR1975459     2  0.6280      0.792 0.000 0.540 0.460
#&gt; SRR1975460     2  0.6280      0.792 0.000 0.540 0.460
#&gt; SRR1975457     2  0.6659      0.789 0.008 0.532 0.460
#&gt; SRR1975458     2  0.6659      0.789 0.008 0.532 0.460
#&gt; SRR1975455     3  0.8405     -0.753 0.084 0.456 0.460
#&gt; SRR1975456     3  0.8405     -0.753 0.084 0.456 0.460
#&gt; SRR1975453     1  0.0000      0.997 1.000 0.000 0.000
#&gt; SRR1975454     1  0.0000      0.997 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-2-a').click(function(){
  $('#tab-MAD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-3'>
<p><a id='tab-MAD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1    p2    p3    p4
#&gt; SRR1975508     3  0.0000      0.996  0 0.000 1.000 0.000
#&gt; SRR1975507     3  0.0000      0.996  0 0.000 1.000 0.000
#&gt; SRR1975506     3  0.0000      0.996  0 0.000 1.000 0.000
#&gt; SRR1975505     3  0.0000      0.996  0 0.000 1.000 0.000
#&gt; SRR1975503     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975504     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975501     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975502     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975499     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975500     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975497     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975493     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975494     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975495     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975491     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975492     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975489     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975490     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975487     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975488     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975485     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975486     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975483     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975477     3  0.0707      0.979  0 0.020 0.980 0.000
#&gt; SRR1975478     3  0.0817      0.975  0 0.024 0.976 0.000
#&gt; SRR1975479     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975480     4  0.0000      0.966  0 0.000 0.000 1.000
#&gt; SRR1975475     4  0.3975      0.711  0 0.240 0.000 0.760
#&gt; SRR1975476     4  0.3569      0.773  0 0.196 0.000 0.804
#&gt; SRR1975473     2  0.4866      0.362  0 0.596 0.404 0.000
#&gt; SRR1975474     2  0.4866      0.362  0 0.596 0.404 0.000
#&gt; SRR1975471     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975469     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975470     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975467     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975468     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975465     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975461     3  0.0000      0.996  0 0.000 1.000 0.000
#&gt; SRR1975462     3  0.0000      0.996  0 0.000 1.000 0.000
#&gt; SRR1975459     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.934  0 1.000 0.000 0.000
#&gt; SRR1975457     3  0.0000      0.996  0 0.000 1.000 0.000
#&gt; SRR1975458     3  0.0000      0.996  0 0.000 1.000 0.000
#&gt; SRR1975455     3  0.0000      0.996  0 0.000 1.000 0.000
#&gt; SRR1975456     3  0.0000      0.996  0 0.000 1.000 0.000
#&gt; SRR1975453     1  0.0000      1.000  1 0.000 0.000 0.000
#&gt; SRR1975454     1  0.0000      1.000  1 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-3-a').click(function(){
  $('#tab-MAD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-4'>
<p><a id='tab-MAD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.0510      1.000 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1975507     3  0.0510      1.000 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1975506     3  0.0510      1.000 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1975505     3  0.0510      1.000 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1975503     4  0.0000      0.971 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975504     4  0.0000      0.971 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975501     1  0.0290      0.994 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1975502     1  0.0290      0.994 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1975499     4  0.0000      0.971 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975500     4  0.0000      0.971 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975497     1  0.0290      0.994 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1975498     1  0.0290      0.994 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1975493     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975494     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975495     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975491     2  0.0290      0.993 0.000 0.992 0.008 0.000 0.000
#&gt; SRR1975492     2  0.0290      0.993 0.000 0.992 0.008 0.000 0.000
#&gt; SRR1975489     4  0.0000      0.971 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975490     4  0.0000      0.971 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975487     4  0.0000      0.971 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975488     4  0.0000      0.971 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975485     4  0.0000      0.971 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975486     4  0.0000      0.971 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975483     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975477     5  0.0000      0.864 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975478     5  0.0000      0.864 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975479     4  0.2707      0.837 0.000 0.000 0.008 0.860 0.132
#&gt; SRR1975480     4  0.2707      0.837 0.000 0.000 0.008 0.860 0.132
#&gt; SRR1975475     5  0.6647      0.275 0.000 0.180 0.008 0.344 0.468
#&gt; SRR1975476     5  0.6594      0.260 0.000 0.168 0.008 0.356 0.468
#&gt; SRR1975473     5  0.0000      0.864 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975474     5  0.0000      0.864 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975471     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975469     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975470     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975467     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975468     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975465     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975461     3  0.0510      1.000 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1975462     3  0.0510      1.000 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1975459     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975457     5  0.0609      0.856 0.000 0.000 0.020 0.000 0.980
#&gt; SRR1975458     5  0.0609      0.856 0.000 0.000 0.020 0.000 0.980
#&gt; SRR1975455     5  0.0290      0.863 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1975456     5  0.0290      0.863 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1975453     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975454     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-4-a').click(function(){
  $('#tab-MAD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-5'>
<p><a id='tab-MAD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975507     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975506     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975505     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975503     4  0.3695     0.5378 0.000 0.000 0.000 0.624 0.000 0.376
#&gt; SRR1975504     4  0.3695     0.5378 0.000 0.000 0.000 0.624 0.000 0.376
#&gt; SRR1975501     1  0.2823     0.8171 0.796 0.000 0.000 0.000 0.000 0.204
#&gt; SRR1975502     1  0.2793     0.8197 0.800 0.000 0.000 0.000 0.000 0.200
#&gt; SRR1975499     4  0.3695     0.5378 0.000 0.000 0.000 0.624 0.000 0.376
#&gt; SRR1975500     4  0.3695     0.5378 0.000 0.000 0.000 0.624 0.000 0.376
#&gt; SRR1975497     1  0.3050     0.7930 0.764 0.000 0.000 0.000 0.000 0.236
#&gt; SRR1975498     1  0.3050     0.7930 0.764 0.000 0.000 0.000 0.000 0.236
#&gt; SRR1975493     2  0.0000     0.9570 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975494     2  0.0000     0.9570 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975495     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975496     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975491     2  0.2793     0.7653 0.000 0.800 0.000 0.000 0.000 0.200
#&gt; SRR1975492     2  0.2793     0.7653 0.000 0.800 0.000 0.000 0.000 0.200
#&gt; SRR1975489     4  0.0146     0.6774 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975490     4  0.0146     0.6774 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1975487     4  0.3198     0.6003 0.000 0.000 0.000 0.740 0.000 0.260
#&gt; SRR1975488     4  0.0000     0.6786 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975485     4  0.0000     0.6786 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975486     4  0.0000     0.6786 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975483     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975482     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975477     5  0.0000     0.9907 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975478     5  0.0000     0.9907 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975479     4  0.4750     0.0124 0.000 0.000 0.000 0.544 0.052 0.404
#&gt; SRR1975480     4  0.4750     0.0124 0.000 0.000 0.000 0.544 0.052 0.404
#&gt; SRR1975475     6  0.4057     0.9917 0.000 0.124 0.000 0.004 0.108 0.764
#&gt; SRR1975476     6  0.4125     0.9917 0.000 0.120 0.000 0.008 0.108 0.764
#&gt; SRR1975473     5  0.0000     0.9907 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975474     5  0.0000     0.9907 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975471     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975472     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975469     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975470     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975467     2  0.0000     0.9570 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975468     2  0.0000     0.9570 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975465     2  0.0000     0.9570 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000     0.9570 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0000     0.9570 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975464     2  0.0000     0.9570 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975461     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975462     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1975459     2  0.0000     0.9570 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000     0.9570 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975457     5  0.0458     0.9847 0.000 0.000 0.016 0.000 0.984 0.000
#&gt; SRR1975458     5  0.0458     0.9847 0.000 0.000 0.016 0.000 0.984 0.000
#&gt; SRR1975455     5  0.0260     0.9904 0.000 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1975456     5  0.0260     0.9904 0.000 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1975453     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1975454     1  0.0000     0.9429 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-5-a').click(function(){
  $('#tab-MAD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-pam-signature_compare](figure_cola/MAD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-pam-collect-classes](figure_cola/MAD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:mclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "mclust"]
# you can also extract it by
# res = res_list["MAD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-mclust-collect-plots](figure_cola/MAD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-mclust-select-partition-number](figure_cola/MAD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.3435 0.657   0.657
#> 3 3 0.597           0.870       0.873         0.7912 0.709   0.557
#> 4 4 0.932           0.975       0.986         0.2329 0.873   0.652
#> 5 5 0.961           0.927       0.966         0.0491 0.945   0.779
#> 6 6 0.905           0.848       0.880         0.0396 0.922   0.655
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 4 5
```

There is also optional best $k$ = 2 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-classes'>
<ul>
<li><a href='#tab-MAD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-mclust-get-classes-1'>
<p><a id='tab-MAD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1975508     2       0          1  0  1
#&gt; SRR1975507     2       0          1  0  1
#&gt; SRR1975506     2       0          1  0  1
#&gt; SRR1975505     2       0          1  0  1
#&gt; SRR1975503     1       0          1  1  0
#&gt; SRR1975504     1       0          1  1  0
#&gt; SRR1975501     1       0          1  1  0
#&gt; SRR1975502     1       0          1  1  0
#&gt; SRR1975499     1       0          1  1  0
#&gt; SRR1975500     1       0          1  1  0
#&gt; SRR1975497     1       0          1  1  0
#&gt; SRR1975498     1       0          1  1  0
#&gt; SRR1975493     1       0          1  1  0
#&gt; SRR1975494     1       0          1  1  0
#&gt; SRR1975495     1       0          1  1  0
#&gt; SRR1975496     1       0          1  1  0
#&gt; SRR1975491     1       0          1  1  0
#&gt; SRR1975492     1       0          1  1  0
#&gt; SRR1975489     1       0          1  1  0
#&gt; SRR1975490     1       0          1  1  0
#&gt; SRR1975487     1       0          1  1  0
#&gt; SRR1975488     1       0          1  1  0
#&gt; SRR1975485     1       0          1  1  0
#&gt; SRR1975486     1       0          1  1  0
#&gt; SRR1975483     1       0          1  1  0
#&gt; SRR1975484     1       0          1  1  0
#&gt; SRR1975481     1       0          1  1  0
#&gt; SRR1975482     1       0          1  1  0
#&gt; SRR1975477     2       0          1  0  1
#&gt; SRR1975478     2       0          1  0  1
#&gt; SRR1975479     1       0          1  1  0
#&gt; SRR1975480     1       0          1  1  0
#&gt; SRR1975475     1       0          1  1  0
#&gt; SRR1975476     1       0          1  1  0
#&gt; SRR1975473     2       0          1  0  1
#&gt; SRR1975474     2       0          1  0  1
#&gt; SRR1975471     1       0          1  1  0
#&gt; SRR1975472     1       0          1  1  0
#&gt; SRR1975469     1       0          1  1  0
#&gt; SRR1975470     1       0          1  1  0
#&gt; SRR1975467     1       0          1  1  0
#&gt; SRR1975468     1       0          1  1  0
#&gt; SRR1975465     1       0          1  1  0
#&gt; SRR1975466     1       0          1  1  0
#&gt; SRR1975463     1       0          1  1  0
#&gt; SRR1975464     1       0          1  1  0
#&gt; SRR1975461     1       0          1  1  0
#&gt; SRR1975462     1       0          1  1  0
#&gt; SRR1975459     1       0          1  1  0
#&gt; SRR1975460     1       0          1  1  0
#&gt; SRR1975457     2       0          1  0  1
#&gt; SRR1975458     2       0          1  0  1
#&gt; SRR1975455     2       0          1  0  1
#&gt; SRR1975456     2       0          1  0  1
#&gt; SRR1975453     1       0          1  1  0
#&gt; SRR1975454     1       0          1  1  0
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-1-a').click(function(){
  $('#tab-MAD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-2'>
<p><a id='tab-MAD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975503     2  0.2959      0.768 0.000 0.900 0.100
#&gt; SRR1975504     2  0.2959      0.768 0.000 0.900 0.100
#&gt; SRR1975501     2  0.0237      0.752 0.004 0.996 0.000
#&gt; SRR1975502     2  0.0237      0.752 0.004 0.996 0.000
#&gt; SRR1975499     2  0.3038      0.767 0.000 0.896 0.104
#&gt; SRR1975500     2  0.3038      0.767 0.000 0.896 0.104
#&gt; SRR1975497     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975498     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975493     2  0.5845      0.702 0.308 0.688 0.004
#&gt; SRR1975494     2  0.5845      0.702 0.308 0.688 0.004
#&gt; SRR1975495     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975496     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975491     2  0.0237      0.752 0.004 0.996 0.000
#&gt; SRR1975492     2  0.0237      0.752 0.004 0.996 0.000
#&gt; SRR1975489     2  0.3587      0.761 0.020 0.892 0.088
#&gt; SRR1975490     2  0.3587      0.761 0.020 0.892 0.088
#&gt; SRR1975487     2  0.3038      0.767 0.000 0.896 0.104
#&gt; SRR1975488     2  0.3038      0.767 0.000 0.896 0.104
#&gt; SRR1975485     2  0.3587      0.761 0.020 0.892 0.088
#&gt; SRR1975486     2  0.3587      0.761 0.020 0.892 0.088
#&gt; SRR1975483     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975484     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975481     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975482     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975477     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975478     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975479     2  0.3587      0.761 0.020 0.892 0.088
#&gt; SRR1975480     2  0.3587      0.761 0.020 0.892 0.088
#&gt; SRR1975475     2  0.3116      0.767 0.000 0.892 0.108
#&gt; SRR1975476     2  0.3116      0.767 0.000 0.892 0.108
#&gt; SRR1975473     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975474     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975471     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975472     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975469     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975470     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975467     2  0.5845      0.702 0.308 0.688 0.004
#&gt; SRR1975468     2  0.5845      0.702 0.308 0.688 0.004
#&gt; SRR1975465     2  0.5845      0.702 0.308 0.688 0.004
#&gt; SRR1975466     2  0.5845      0.702 0.308 0.688 0.004
#&gt; SRR1975463     2  0.5845      0.702 0.308 0.688 0.004
#&gt; SRR1975464     2  0.5845      0.702 0.308 0.688 0.004
#&gt; SRR1975461     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975462     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975459     2  0.5845      0.702 0.308 0.688 0.004
#&gt; SRR1975460     2  0.5845      0.702 0.308 0.688 0.004
#&gt; SRR1975457     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975458     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975455     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975456     3  0.0000      1.000 0.000 0.000 1.000
#&gt; SRR1975453     1  0.5815      1.000 0.692 0.304 0.004
#&gt; SRR1975454     1  0.5815      1.000 0.692 0.304 0.004
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-2-a').click(function(){
  $('#tab-MAD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-3'>
<p><a id='tab-MAD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975503     4  0.0336      0.992 0.000 0.008 0.000 0.992
#&gt; SRR1975504     4  0.0336      0.992 0.000 0.008 0.000 0.992
#&gt; SRR1975501     2  0.3356      0.835 0.176 0.824 0.000 0.000
#&gt; SRR1975502     2  0.3356      0.835 0.176 0.824 0.000 0.000
#&gt; SRR1975499     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975500     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975497     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975493     2  0.0000      0.940 0.000 1.000 0.000 0.000
#&gt; SRR1975494     2  0.0000      0.940 0.000 1.000 0.000 0.000
#&gt; SRR1975495     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975491     2  0.3356      0.835 0.176 0.824 0.000 0.000
#&gt; SRR1975492     2  0.3356      0.835 0.176 0.824 0.000 0.000
#&gt; SRR1975489     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975487     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975488     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975485     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975486     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975483     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975477     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975478     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975479     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975480     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975475     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975476     4  0.0000      0.999 0.000 0.000 0.000 1.000
#&gt; SRR1975473     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975474     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975471     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975469     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975470     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975467     2  0.0000      0.940 0.000 1.000 0.000 0.000
#&gt; SRR1975468     2  0.0000      0.940 0.000 1.000 0.000 0.000
#&gt; SRR1975465     2  0.0000      0.940 0.000 1.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.940 0.000 1.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.940 0.000 1.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.940 0.000 1.000 0.000 0.000
#&gt; SRR1975461     1  0.1022      0.968 0.968 0.000 0.032 0.000
#&gt; SRR1975462     1  0.1022      0.968 0.968 0.000 0.032 0.000
#&gt; SRR1975459     2  0.0000      0.940 0.000 1.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.940 0.000 1.000 0.000 0.000
#&gt; SRR1975457     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975458     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975455     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975456     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975453     1  0.0000      0.996 1.000 0.000 0.000 0.000
#&gt; SRR1975454     1  0.0000      0.996 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-3-a').click(function(){
  $('#tab-MAD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-4'>
<p><a id='tab-MAD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1    p2 p3   p4    p5
#&gt; SRR1975508     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975507     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975506     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975505     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975503     5   0.439      0.425  0 0.008  0 0.38 0.612
#&gt; SRR1975504     5   0.439      0.425  0 0.008  0 0.38 0.612
#&gt; SRR1975501     5   0.000      0.766  0 0.000  0 0.00 1.000
#&gt; SRR1975502     5   0.000      0.766  0 0.000  0 0.00 1.000
#&gt; SRR1975499     4   0.311      0.721  0 0.000  0 0.80 0.200
#&gt; SRR1975500     4   0.311      0.721  0 0.000  0 0.80 0.200
#&gt; SRR1975497     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975498     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975493     2   0.000      1.000  0 1.000  0 0.00 0.000
#&gt; SRR1975494     2   0.000      1.000  0 1.000  0 0.00 0.000
#&gt; SRR1975495     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975496     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975491     5   0.000      0.766  0 0.000  0 0.00 1.000
#&gt; SRR1975492     5   0.000      0.766  0 0.000  0 0.00 1.000
#&gt; SRR1975489     4   0.000      0.955  0 0.000  0 1.00 0.000
#&gt; SRR1975490     4   0.000      0.955  0 0.000  0 1.00 0.000
#&gt; SRR1975487     4   0.000      0.955  0 0.000  0 1.00 0.000
#&gt; SRR1975488     4   0.000      0.955  0 0.000  0 1.00 0.000
#&gt; SRR1975485     4   0.000      0.955  0 0.000  0 1.00 0.000
#&gt; SRR1975486     4   0.000      0.955  0 0.000  0 1.00 0.000
#&gt; SRR1975483     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975484     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975481     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975482     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975477     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975478     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975479     4   0.000      0.955  0 0.000  0 1.00 0.000
#&gt; SRR1975480     4   0.000      0.955  0 0.000  0 1.00 0.000
#&gt; SRR1975475     4   0.000      0.955  0 0.000  0 1.00 0.000
#&gt; SRR1975476     4   0.000      0.955  0 0.000  0 1.00 0.000
#&gt; SRR1975473     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975474     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975471     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975472     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975469     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975470     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975467     5   0.405      0.504  0 0.356  0 0.00 0.644
#&gt; SRR1975468     5   0.405      0.504  0 0.356  0 0.00 0.644
#&gt; SRR1975465     2   0.000      1.000  0 1.000  0 0.00 0.000
#&gt; SRR1975466     2   0.000      1.000  0 1.000  0 0.00 0.000
#&gt; SRR1975463     2   0.000      1.000  0 1.000  0 0.00 0.000
#&gt; SRR1975464     2   0.000      1.000  0 1.000  0 0.00 0.000
#&gt; SRR1975461     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975462     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975459     2   0.000      1.000  0 1.000  0 0.00 0.000
#&gt; SRR1975460     2   0.000      1.000  0 1.000  0 0.00 0.000
#&gt; SRR1975457     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975458     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975455     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975456     3   0.000      1.000  0 0.000  1 0.00 0.000
#&gt; SRR1975453     1   0.000      1.000  1 0.000  0 0.00 0.000
#&gt; SRR1975454     1   0.000      1.000  1 0.000  0 0.00 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-4-a').click(function(){
  $('#tab-MAD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-5'>
<p><a id='tab-MAD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5    p6
#&gt; SRR1975508     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975507     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975506     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975505     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975503     4   0.633    -0.0430 0.000 0.008 0.300 0.356  0 0.336
#&gt; SRR1975504     4   0.633    -0.0430 0.000 0.008 0.300 0.356  0 0.336
#&gt; SRR1975501     6   0.000     1.0000 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975502     6   0.000     1.0000 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975499     4   0.369     0.7042 0.000 0.000 0.076 0.784  0 0.140
#&gt; SRR1975500     4   0.369     0.7042 0.000 0.000 0.076 0.784  0 0.140
#&gt; SRR1975497     1   0.000     0.9372 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975498     1   0.000     0.9372 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975493     2   0.000     0.8508 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975494     2   0.000     0.8508 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975495     1   0.270     0.6736 0.812 0.000 0.188 0.000  0 0.000
#&gt; SRR1975496     1   0.270     0.6736 0.812 0.000 0.188 0.000  0 0.000
#&gt; SRR1975491     6   0.000     1.0000 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975492     6   0.000     1.0000 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1975489     4   0.000     0.8641 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975490     4   0.000     0.8641 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975487     4   0.000     0.8641 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975488     4   0.000     0.8641 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975485     4   0.000     0.8641 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975486     4   0.000     0.8641 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975483     1   0.000     0.9372 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975484     1   0.000     0.9372 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975481     1   0.000     0.9372 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975482     1   0.000     0.9372 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975477     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975478     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975479     4   0.000     0.8641 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975480     4   0.000     0.8641 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975475     4   0.000     0.8641 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975476     4   0.000     0.8641 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1975473     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975474     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975471     3   0.341     1.0000 0.300 0.000 0.700 0.000  0 0.000
#&gt; SRR1975472     3   0.341     1.0000 0.300 0.000 0.700 0.000  0 0.000
#&gt; SRR1975469     1   0.000     0.9372 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975470     1   0.000     0.9372 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1975467     2   0.612    -0.0672 0.000 0.356 0.300 0.000  0 0.344
#&gt; SRR1975468     2   0.612    -0.0672 0.000 0.356 0.300 0.000  0 0.344
#&gt; SRR1975465     2   0.000     0.8508 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975466     2   0.000     0.8508 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975463     2   0.000     0.8508 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975464     2   0.000     0.8508 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975461     3   0.341     1.0000 0.300 0.000 0.700 0.000  0 0.000
#&gt; SRR1975462     3   0.341     1.0000 0.300 0.000 0.700 0.000  0 0.000
#&gt; SRR1975459     2   0.000     0.8508 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975460     2   0.000     0.8508 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1975457     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975458     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975455     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975456     5   0.000     1.0000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1975453     3   0.341     1.0000 0.300 0.000 0.700 0.000  0 0.000
#&gt; SRR1975454     3   0.341     1.0000 0.300 0.000 0.700 0.000  0 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-5-a').click(function(){
  $('#tab-MAD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-mclust-signature_compare](figure_cola/MAD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-mclust-collect-classes](figure_cola/MAD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:NMF






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "NMF"]
# you can also extract it by
# res = res_list["MAD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-NMF-collect-plots](figure_cola/MAD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-NMF-select-partition-number](figure_cola/MAD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.890           0.913       0.966         0.5070 0.492   0.492
#> 3 3 0.648           0.658       0.838         0.3005 0.751   0.543
#> 4 4 0.679           0.760       0.847         0.1178 0.756   0.416
#> 5 5 0.645           0.659       0.801         0.0579 0.868   0.549
#> 6 6 0.655           0.623       0.760         0.0364 0.940   0.739
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-classes'>
<ul>
<li><a href='#tab-MAD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-NMF-get-classes-1'>
<p><a id='tab-MAD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975507     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975506     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975505     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975503     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975504     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975501     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975502     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975499     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975500     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975497     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975498     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975493     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975494     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975495     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975496     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975491     1   0.482     0.8654 0.896 0.104
#&gt; SRR1975492     1   0.574     0.8326 0.864 0.136
#&gt; SRR1975489     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975490     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975487     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975488     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975485     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975486     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975483     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975484     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975481     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975482     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975477     1   0.850     0.6364 0.724 0.276
#&gt; SRR1975478     1   0.861     0.6225 0.716 0.284
#&gt; SRR1975479     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975480     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975475     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975476     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975473     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975474     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975471     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975472     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975469     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975470     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975467     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975468     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975465     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975466     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975463     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975464     1   0.000     0.9526 1.000 0.000
#&gt; SRR1975461     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975462     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975459     1   0.999     0.0907 0.520 0.480
#&gt; SRR1975460     2   1.000    -0.0660 0.496 0.504
#&gt; SRR1975457     2   0.141     0.9603 0.020 0.980
#&gt; SRR1975458     2   0.141     0.9603 0.020 0.980
#&gt; SRR1975455     2   0.204     0.9492 0.032 0.968
#&gt; SRR1975456     2   0.184     0.9531 0.028 0.972
#&gt; SRR1975453     2   0.000     0.9755 0.000 1.000
#&gt; SRR1975454     2   0.000     0.9755 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-1-a').click(function(){
  $('#tab-MAD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-2'>
<p><a id='tab-MAD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3   0.571      0.671 0.320 0.000 0.680
#&gt; SRR1975507     3   0.583      0.658 0.340 0.000 0.660
#&gt; SRR1975506     3   0.593      0.647 0.356 0.000 0.644
#&gt; SRR1975505     3   0.606      0.623 0.384 0.000 0.616
#&gt; SRR1975503     1   0.617      0.354 0.588 0.412 0.000
#&gt; SRR1975504     1   0.617      0.354 0.588 0.412 0.000
#&gt; SRR1975501     2   0.610      0.339 0.000 0.608 0.392
#&gt; SRR1975502     2   0.610      0.339 0.000 0.608 0.392
#&gt; SRR1975499     1   0.617      0.354 0.588 0.412 0.000
#&gt; SRR1975500     1   0.617      0.354 0.588 0.412 0.000
#&gt; SRR1975497     3   0.304      0.735 0.000 0.104 0.896
#&gt; SRR1975498     3   0.304      0.735 0.000 0.104 0.896
#&gt; SRR1975493     2   0.254      0.761 0.080 0.920 0.000
#&gt; SRR1975494     2   0.254      0.761 0.080 0.920 0.000
#&gt; SRR1975495     3   0.236      0.763 0.000 0.072 0.928
#&gt; SRR1975496     3   0.245      0.760 0.000 0.076 0.924
#&gt; SRR1975491     2   0.000      0.769 0.000 1.000 0.000
#&gt; SRR1975492     2   0.000      0.769 0.000 1.000 0.000
#&gt; SRR1975489     1   0.000      0.752 1.000 0.000 0.000
#&gt; SRR1975490     1   0.000      0.752 1.000 0.000 0.000
#&gt; SRR1975487     1   0.610      0.385 0.608 0.392 0.000
#&gt; SRR1975488     1   0.603      0.409 0.624 0.376 0.000
#&gt; SRR1975485     1   0.000      0.752 1.000 0.000 0.000
#&gt; SRR1975486     1   0.000      0.752 1.000 0.000 0.000
#&gt; SRR1975483     3   0.000      0.805 0.000 0.000 1.000
#&gt; SRR1975484     3   0.000      0.805 0.000 0.000 1.000
#&gt; SRR1975481     3   0.000      0.805 0.000 0.000 1.000
#&gt; SRR1975482     3   0.000      0.805 0.000 0.000 1.000
#&gt; SRR1975477     3   0.630      0.480 0.476 0.000 0.524
#&gt; SRR1975478     3   0.630      0.480 0.476 0.000 0.524
#&gt; SRR1975479     1   0.000      0.752 1.000 0.000 0.000
#&gt; SRR1975480     1   0.000      0.752 1.000 0.000 0.000
#&gt; SRR1975475     1   0.000      0.752 1.000 0.000 0.000
#&gt; SRR1975476     1   0.000      0.752 1.000 0.000 0.000
#&gt; SRR1975473     1   0.263      0.678 0.916 0.000 0.084
#&gt; SRR1975474     1   0.263      0.678 0.916 0.000 0.084
#&gt; SRR1975471     3   0.000      0.805 0.000 0.000 1.000
#&gt; SRR1975472     3   0.000      0.805 0.000 0.000 1.000
#&gt; SRR1975469     3   0.000      0.805 0.000 0.000 1.000
#&gt; SRR1975470     3   0.000      0.805 0.000 0.000 1.000
#&gt; SRR1975467     2   0.615      0.178 0.408 0.592 0.000
#&gt; SRR1975468     2   0.615      0.178 0.408 0.592 0.000
#&gt; SRR1975465     2   0.175      0.772 0.048 0.952 0.000
#&gt; SRR1975466     2   0.175      0.772 0.048 0.952 0.000
#&gt; SRR1975463     2   0.388      0.704 0.152 0.848 0.000
#&gt; SRR1975464     2   0.388      0.704 0.152 0.848 0.000
#&gt; SRR1975461     3   0.000      0.805 0.000 0.000 1.000
#&gt; SRR1975462     3   0.000      0.805 0.000 0.000 1.000
#&gt; SRR1975459     2   0.000      0.769 0.000 1.000 0.000
#&gt; SRR1975460     2   0.000      0.769 0.000 1.000 0.000
#&gt; SRR1975457     3   0.604      0.627 0.380 0.000 0.620
#&gt; SRR1975458     3   0.604      0.627 0.380 0.000 0.620
#&gt; SRR1975455     3   0.610      0.614 0.392 0.000 0.608
#&gt; SRR1975456     3   0.610      0.614 0.392 0.000 0.608
#&gt; SRR1975453     3   0.000      0.805 0.000 0.000 1.000
#&gt; SRR1975454     3   0.000      0.805 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-2-a').click(function(){
  $('#tab-MAD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-3'>
<p><a id='tab-MAD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.1042      0.929 0.000 0.020 0.972 0.008
#&gt; SRR1975507     3  0.0895      0.929 0.000 0.020 0.976 0.004
#&gt; SRR1975506     3  0.0895      0.929 0.000 0.020 0.976 0.004
#&gt; SRR1975505     3  0.1042      0.929 0.000 0.020 0.972 0.008
#&gt; SRR1975503     2  0.2611      0.882 0.008 0.896 0.000 0.096
#&gt; SRR1975504     2  0.2611      0.882 0.008 0.896 0.000 0.096
#&gt; SRR1975501     1  0.2530      0.562 0.896 0.100 0.004 0.000
#&gt; SRR1975502     1  0.2530      0.562 0.896 0.100 0.004 0.000
#&gt; SRR1975499     2  0.2799      0.877 0.008 0.884 0.000 0.108
#&gt; SRR1975500     2  0.2799      0.877 0.008 0.884 0.000 0.108
#&gt; SRR1975497     1  0.2760      0.654 0.872 0.000 0.128 0.000
#&gt; SRR1975498     1  0.2760      0.654 0.872 0.000 0.128 0.000
#&gt; SRR1975493     2  0.2214      0.892 0.044 0.928 0.000 0.028
#&gt; SRR1975494     2  0.2214      0.892 0.044 0.928 0.000 0.028
#&gt; SRR1975495     1  0.4399      0.668 0.760 0.016 0.224 0.000
#&gt; SRR1975496     1  0.4399      0.668 0.760 0.016 0.224 0.000
#&gt; SRR1975491     1  0.4972     -0.158 0.544 0.456 0.000 0.000
#&gt; SRR1975492     1  0.4972     -0.158 0.544 0.456 0.000 0.000
#&gt; SRR1975489     4  0.0859      0.910 0.008 0.008 0.004 0.980
#&gt; SRR1975490     4  0.0992      0.909 0.012 0.008 0.004 0.976
#&gt; SRR1975487     2  0.3933      0.793 0.008 0.792 0.000 0.200
#&gt; SRR1975488     2  0.4360      0.729 0.008 0.744 0.000 0.248
#&gt; SRR1975485     4  0.1114      0.909 0.004 0.008 0.016 0.972
#&gt; SRR1975486     4  0.1114      0.909 0.004 0.008 0.016 0.972
#&gt; SRR1975483     1  0.4876      0.644 0.672 0.004 0.320 0.004
#&gt; SRR1975484     1  0.4876      0.644 0.672 0.004 0.320 0.004
#&gt; SRR1975481     1  0.4991      0.645 0.672 0.004 0.316 0.008
#&gt; SRR1975482     1  0.4991      0.645 0.672 0.004 0.316 0.008
#&gt; SRR1975477     3  0.4033      0.778 0.008 0.020 0.824 0.148
#&gt; SRR1975478     3  0.4033      0.778 0.008 0.020 0.824 0.148
#&gt; SRR1975479     4  0.0992      0.910 0.012 0.008 0.004 0.976
#&gt; SRR1975480     4  0.0992      0.910 0.012 0.008 0.004 0.976
#&gt; SRR1975475     4  0.5133      0.655 0.004 0.268 0.024 0.704
#&gt; SRR1975476     4  0.5076      0.669 0.004 0.260 0.024 0.712
#&gt; SRR1975473     4  0.2179      0.877 0.000 0.012 0.064 0.924
#&gt; SRR1975474     4  0.2179      0.877 0.000 0.012 0.064 0.924
#&gt; SRR1975471     1  0.5335      0.432 0.504 0.004 0.488 0.004
#&gt; SRR1975472     1  0.5335      0.432 0.504 0.004 0.488 0.004
#&gt; SRR1975469     1  0.5461      0.427 0.508 0.004 0.480 0.008
#&gt; SRR1975470     1  0.5463      0.412 0.500 0.004 0.488 0.008
#&gt; SRR1975467     2  0.1396      0.899 0.004 0.960 0.004 0.032
#&gt; SRR1975468     2  0.1396      0.899 0.004 0.960 0.004 0.032
#&gt; SRR1975465     2  0.1388      0.891 0.012 0.960 0.028 0.000
#&gt; SRR1975466     2  0.1510      0.890 0.016 0.956 0.028 0.000
#&gt; SRR1975463     2  0.1443      0.895 0.004 0.960 0.028 0.008
#&gt; SRR1975464     2  0.1443      0.895 0.004 0.960 0.028 0.008
#&gt; SRR1975461     3  0.1297      0.915 0.020 0.016 0.964 0.000
#&gt; SRR1975462     3  0.1297      0.915 0.020 0.016 0.964 0.000
#&gt; SRR1975459     2  0.4467      0.782 0.172 0.788 0.040 0.000
#&gt; SRR1975460     2  0.4467      0.782 0.172 0.788 0.040 0.000
#&gt; SRR1975457     3  0.1174      0.927 0.000 0.020 0.968 0.012
#&gt; SRR1975458     3  0.1174      0.927 0.000 0.020 0.968 0.012
#&gt; SRR1975455     3  0.0895      0.925 0.000 0.004 0.976 0.020
#&gt; SRR1975456     3  0.0895      0.925 0.000 0.004 0.976 0.020
#&gt; SRR1975453     3  0.2125      0.851 0.076 0.000 0.920 0.004
#&gt; SRR1975454     3  0.2125      0.851 0.076 0.000 0.920 0.004
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-3-a').click(function(){
  $('#tab-MAD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-4'>
<p><a id='tab-MAD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.2179      0.741 0.000 0.072 0.912 0.008 0.008
#&gt; SRR1975507     3  0.1770      0.748 0.000 0.048 0.936 0.008 0.008
#&gt; SRR1975506     3  0.1770      0.748 0.000 0.048 0.936 0.008 0.008
#&gt; SRR1975505     3  0.2115      0.743 0.000 0.068 0.916 0.008 0.008
#&gt; SRR1975503     5  0.4249      0.651 0.000 0.432 0.000 0.000 0.568
#&gt; SRR1975504     5  0.4249      0.651 0.000 0.432 0.000 0.000 0.568
#&gt; SRR1975501     1  0.4792      0.375 0.712 0.228 0.008 0.000 0.052
#&gt; SRR1975502     1  0.4792      0.375 0.712 0.228 0.008 0.000 0.052
#&gt; SRR1975499     5  0.4025      0.781 0.000 0.292 0.000 0.008 0.700
#&gt; SRR1975500     5  0.3928      0.780 0.000 0.296 0.000 0.004 0.700
#&gt; SRR1975497     1  0.2629      0.760 0.860 0.000 0.136 0.000 0.004
#&gt; SRR1975498     1  0.2583      0.758 0.864 0.000 0.132 0.000 0.004
#&gt; SRR1975493     2  0.1018      0.804 0.016 0.968 0.000 0.000 0.016
#&gt; SRR1975494     2  0.1018      0.804 0.016 0.968 0.000 0.000 0.016
#&gt; SRR1975495     1  0.2930      0.763 0.832 0.004 0.164 0.000 0.000
#&gt; SRR1975496     1  0.2930      0.763 0.832 0.004 0.164 0.000 0.000
#&gt; SRR1975491     2  0.4687      0.482 0.336 0.636 0.000 0.000 0.028
#&gt; SRR1975492     2  0.4687      0.482 0.336 0.636 0.000 0.000 0.028
#&gt; SRR1975489     4  0.2536      0.757 0.000 0.004 0.000 0.868 0.128
#&gt; SRR1975490     4  0.2536      0.757 0.000 0.004 0.000 0.868 0.128
#&gt; SRR1975487     5  0.3165      0.704 0.000 0.116 0.000 0.036 0.848
#&gt; SRR1975488     5  0.3255      0.683 0.000 0.100 0.000 0.052 0.848
#&gt; SRR1975485     4  0.2966      0.759 0.000 0.000 0.000 0.816 0.184
#&gt; SRR1975486     4  0.2966      0.759 0.000 0.000 0.000 0.816 0.184
#&gt; SRR1975483     1  0.4546      0.681 0.668 0.000 0.304 0.000 0.028
#&gt; SRR1975484     1  0.4546      0.681 0.668 0.000 0.304 0.000 0.028
#&gt; SRR1975481     1  0.5225      0.690 0.652 0.000 0.288 0.016 0.044
#&gt; SRR1975482     1  0.5225      0.690 0.652 0.000 0.288 0.016 0.044
#&gt; SRR1975477     3  0.6863      0.121 0.008 0.156 0.468 0.356 0.012
#&gt; SRR1975478     3  0.6863      0.121 0.008 0.156 0.468 0.356 0.012
#&gt; SRR1975479     4  0.0579      0.794 0.000 0.000 0.008 0.984 0.008
#&gt; SRR1975480     4  0.0579      0.794 0.000 0.000 0.008 0.984 0.008
#&gt; SRR1975475     4  0.7469      0.390 0.008 0.244 0.036 0.468 0.244
#&gt; SRR1975476     4  0.7452      0.397 0.008 0.240 0.036 0.472 0.244
#&gt; SRR1975473     4  0.2833      0.771 0.000 0.020 0.068 0.888 0.024
#&gt; SRR1975474     4  0.2833      0.771 0.000 0.020 0.068 0.888 0.024
#&gt; SRR1975471     3  0.4687      0.282 0.336 0.000 0.636 0.000 0.028
#&gt; SRR1975472     3  0.4687      0.282 0.336 0.000 0.636 0.000 0.028
#&gt; SRR1975469     3  0.5162      0.374 0.276 0.000 0.664 0.016 0.044
#&gt; SRR1975470     3  0.5162      0.374 0.276 0.000 0.664 0.016 0.044
#&gt; SRR1975467     2  0.2694      0.746 0.008 0.892 0.032 0.000 0.068
#&gt; SRR1975468     2  0.2694      0.746 0.008 0.892 0.032 0.000 0.068
#&gt; SRR1975465     2  0.1251      0.815 0.000 0.956 0.036 0.000 0.008
#&gt; SRR1975466     2  0.1251      0.815 0.000 0.956 0.036 0.000 0.008
#&gt; SRR1975463     2  0.1202      0.813 0.004 0.960 0.032 0.000 0.004
#&gt; SRR1975464     2  0.1202      0.813 0.004 0.960 0.032 0.000 0.004
#&gt; SRR1975461     3  0.1764      0.733 0.036 0.012 0.940 0.000 0.012
#&gt; SRR1975462     3  0.1764      0.733 0.036 0.012 0.940 0.000 0.012
#&gt; SRR1975459     2  0.3691      0.762 0.072 0.844 0.028 0.000 0.056
#&gt; SRR1975460     2  0.3691      0.762 0.072 0.844 0.028 0.000 0.056
#&gt; SRR1975457     3  0.3169      0.695 0.000 0.140 0.840 0.016 0.004
#&gt; SRR1975458     3  0.3169      0.695 0.000 0.140 0.840 0.016 0.004
#&gt; SRR1975455     3  0.1560      0.748 0.000 0.028 0.948 0.020 0.004
#&gt; SRR1975456     3  0.1560      0.748 0.000 0.028 0.948 0.020 0.004
#&gt; SRR1975453     3  0.1774      0.714 0.052 0.000 0.932 0.000 0.016
#&gt; SRR1975454     3  0.1774      0.714 0.052 0.000 0.932 0.000 0.016
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-4-a').click(function(){
  $('#tab-MAD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-5'>
<p><a id='tab-MAD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     3   0.159      0.802 0.000 0.052 0.932 0.000 0.016 0.000
#&gt; SRR1975507     3   0.139      0.806 0.000 0.040 0.944 0.000 0.016 0.000
#&gt; SRR1975506     3   0.139      0.806 0.000 0.040 0.944 0.000 0.016 0.000
#&gt; SRR1975505     3   0.155      0.805 0.000 0.044 0.936 0.000 0.020 0.000
#&gt; SRR1975503     4   0.478      0.714 0.000 0.276 0.000 0.644 0.076 0.004
#&gt; SRR1975504     4   0.480      0.708 0.000 0.280 0.000 0.640 0.076 0.004
#&gt; SRR1975501     2   0.536      0.256 0.460 0.464 0.008 0.008 0.060 0.000
#&gt; SRR1975502     2   0.536      0.256 0.460 0.464 0.008 0.008 0.060 0.000
#&gt; SRR1975499     4   0.354      0.794 0.000 0.160 0.000 0.788 0.052 0.000
#&gt; SRR1975500     4   0.354      0.794 0.000 0.160 0.000 0.788 0.052 0.000
#&gt; SRR1975497     1   0.158      0.650 0.936 0.000 0.048 0.000 0.012 0.004
#&gt; SRR1975498     1   0.143      0.650 0.940 0.000 0.048 0.000 0.012 0.000
#&gt; SRR1975493     2   0.214      0.730 0.004 0.908 0.000 0.036 0.052 0.000
#&gt; SRR1975494     2   0.214      0.730 0.004 0.908 0.000 0.036 0.052 0.000
#&gt; SRR1975495     1   0.231      0.676 0.884 0.000 0.100 0.004 0.012 0.000
#&gt; SRR1975496     1   0.231      0.676 0.884 0.000 0.100 0.004 0.012 0.000
#&gt; SRR1975491     2   0.376      0.679 0.104 0.808 0.000 0.024 0.064 0.000
#&gt; SRR1975492     2   0.376      0.679 0.104 0.808 0.000 0.024 0.064 0.000
#&gt; SRR1975489     6   0.161      0.581 0.000 0.000 0.000 0.084 0.000 0.916
#&gt; SRR1975490     6   0.161      0.581 0.000 0.000 0.000 0.084 0.000 0.916
#&gt; SRR1975487     4   0.193      0.678 0.000 0.016 0.000 0.924 0.020 0.040
#&gt; SRR1975488     4   0.191      0.673 0.000 0.012 0.000 0.924 0.020 0.044
#&gt; SRR1975485     6   0.569      0.332 0.000 0.000 0.000 0.216 0.260 0.524
#&gt; SRR1975486     6   0.569      0.332 0.000 0.000 0.000 0.216 0.260 0.524
#&gt; SRR1975483     1   0.566      0.521 0.516 0.000 0.368 0.012 0.100 0.004
#&gt; SRR1975484     1   0.566      0.521 0.516 0.000 0.368 0.012 0.100 0.004
#&gt; SRR1975481     1   0.683      0.517 0.432 0.000 0.296 0.012 0.228 0.032
#&gt; SRR1975482     1   0.682      0.516 0.432 0.000 0.300 0.012 0.224 0.032
#&gt; SRR1975477     5   0.664      0.610 0.000 0.080 0.252 0.004 0.520 0.144
#&gt; SRR1975478     5   0.664      0.610 0.000 0.080 0.252 0.004 0.520 0.144
#&gt; SRR1975479     6   0.274      0.569 0.000 0.000 0.004 0.000 0.176 0.820
#&gt; SRR1975480     6   0.274      0.569 0.000 0.000 0.004 0.000 0.176 0.820
#&gt; SRR1975475     5   0.535      0.540 0.000 0.092 0.008 0.040 0.680 0.180
#&gt; SRR1975476     5   0.535      0.540 0.000 0.092 0.008 0.040 0.680 0.180
#&gt; SRR1975473     6   0.478      0.328 0.004 0.016 0.016 0.004 0.372 0.588
#&gt; SRR1975474     6   0.479      0.328 0.004 0.016 0.016 0.004 0.376 0.584
#&gt; SRR1975471     3   0.492      0.495 0.184 0.000 0.692 0.012 0.108 0.004
#&gt; SRR1975472     3   0.492      0.495 0.184 0.000 0.692 0.012 0.108 0.004
#&gt; SRR1975469     3   0.609      0.394 0.108 0.000 0.600 0.012 0.228 0.052
#&gt; SRR1975470     3   0.609      0.394 0.108 0.000 0.600 0.012 0.228 0.052
#&gt; SRR1975467     2   0.466      0.487 0.000 0.660 0.016 0.044 0.280 0.000
#&gt; SRR1975468     2   0.464      0.493 0.000 0.664 0.016 0.044 0.276 0.000
#&gt; SRR1975465     2   0.220      0.738 0.000 0.900 0.048 0.000 0.052 0.000
#&gt; SRR1975466     2   0.220      0.738 0.000 0.900 0.048 0.000 0.052 0.000
#&gt; SRR1975463     2   0.268      0.723 0.000 0.876 0.020 0.020 0.084 0.000
#&gt; SRR1975464     2   0.268      0.723 0.000 0.876 0.020 0.020 0.084 0.000
#&gt; SRR1975461     3   0.126      0.800 0.016 0.020 0.956 0.000 0.008 0.000
#&gt; SRR1975462     3   0.126      0.800 0.016 0.020 0.956 0.000 0.008 0.000
#&gt; SRR1975459     2   0.280      0.719 0.024 0.876 0.064 0.000 0.036 0.000
#&gt; SRR1975460     2   0.288      0.718 0.028 0.872 0.064 0.000 0.036 0.000
#&gt; SRR1975457     3   0.316      0.738 0.000 0.080 0.844 0.000 0.068 0.008
#&gt; SRR1975458     3   0.316      0.738 0.000 0.080 0.844 0.000 0.068 0.008
#&gt; SRR1975455     3   0.236      0.791 0.000 0.028 0.900 0.000 0.056 0.016
#&gt; SRR1975456     3   0.236      0.791 0.000 0.028 0.900 0.000 0.056 0.016
#&gt; SRR1975453     3   0.156      0.784 0.032 0.004 0.940 0.000 0.024 0.000
#&gt; SRR1975454     3   0.156      0.784 0.032 0.004 0.940 0.000 0.024 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-5-a').click(function(){
  $('#tab-MAD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-NMF-signature_compare](figure_cola/MAD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-NMF-collect-classes](figure_cola/MAD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "hclust"]
# you can also extract it by
# res = res_list["ATC:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-hclust-collect-plots](figure_cola/ATC-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-hclust-select-partition-number](figure_cola/ATC-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.951       0.979         0.1692 0.805   0.805
#> 3 3 0.869           0.894       0.961         2.3815 0.579   0.494
#> 4 4 0.874           0.886       0.960         0.0488 0.953   0.893
#> 5 5 0.816           0.773       0.869         0.1266 0.899   0.748
#> 6 6 0.869           0.861       0.936         0.0412 0.979   0.934
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-classes'>
<ul>
<li><a href='#tab-ATC-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-hclust-get-classes-1'>
<p><a id='tab-ATC-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.0000      0.796 0.000 1.000
#&gt; SRR1975507     2  0.0000      0.796 0.000 1.000
#&gt; SRR1975506     2  0.0000      0.796 0.000 1.000
#&gt; SRR1975505     2  0.0000      0.796 0.000 1.000
#&gt; SRR1975503     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975504     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975501     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975502     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975499     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975500     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975497     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975498     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975493     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975494     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975495     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975496     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975491     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975492     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975489     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975490     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975487     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975488     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975485     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975486     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975483     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975484     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975481     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975482     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975477     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975478     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975479     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975480     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975475     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975476     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975473     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975474     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975471     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975472     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975469     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975470     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975467     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975468     1  0.0000      0.995 1.000 0.000
#&gt; SRR1975465     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975466     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975463     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975464     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975461     2  1.0000      0.199 0.496 0.504
#&gt; SRR1975462     2  1.0000      0.199 0.496 0.504
#&gt; SRR1975459     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975460     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975457     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975458     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975455     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975456     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975453     1  0.0938      0.990 0.988 0.012
#&gt; SRR1975454     1  0.0938      0.990 0.988 0.012
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-1-a').click(function(){
  $('#tab-ATC-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-2'>
<p><a id='tab-ATC-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975507     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975506     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975505     3  0.0000     1.0000 0.000 0.000 1.000
#&gt; SRR1975503     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975504     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975501     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975502     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975499     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975500     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975497     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975498     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975493     2  0.1753     0.8681 0.048 0.952 0.000
#&gt; SRR1975494     2  0.1753     0.8681 0.048 0.952 0.000
#&gt; SRR1975495     1  0.5431     0.5799 0.716 0.284 0.000
#&gt; SRR1975496     1  0.5431     0.5799 0.716 0.284 0.000
#&gt; SRR1975491     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975492     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975489     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975490     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975487     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975488     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975485     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975486     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975483     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975484     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975481     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975482     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975477     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975478     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975479     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975480     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975475     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975476     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975473     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975474     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975471     2  0.5138     0.5989 0.252 0.748 0.000
#&gt; SRR1975472     2  0.5138     0.5989 0.252 0.748 0.000
#&gt; SRR1975469     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975470     1  0.0000     0.9753 1.000 0.000 0.000
#&gt; SRR1975467     1  0.0237     0.9715 0.996 0.004 0.000
#&gt; SRR1975468     1  0.0237     0.9715 0.996 0.004 0.000
#&gt; SRR1975465     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975466     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975463     2  0.0424     0.9027 0.008 0.992 0.000
#&gt; SRR1975464     2  0.0424     0.9027 0.008 0.992 0.000
#&gt; SRR1975461     2  0.6308     0.0728 0.000 0.508 0.492
#&gt; SRR1975462     2  0.6308     0.0728 0.000 0.508 0.492
#&gt; SRR1975459     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975460     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975457     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975458     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975455     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975456     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975453     2  0.0000     0.9075 0.000 1.000 0.000
#&gt; SRR1975454     2  0.0000     0.9075 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-2-a').click(function(){
  $('#tab-ATC-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-3'>
<p><a id='tab-ATC-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975503     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975504     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975501     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975502     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975499     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975500     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975497     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975498     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975493     2  0.1677      0.873 0.012 0.948 0.000 0.040
#&gt; SRR1975494     2  0.1677      0.873 0.012 0.948 0.000 0.040
#&gt; SRR1975495     4  0.4621      0.566 0.008 0.284 0.000 0.708
#&gt; SRR1975496     4  0.4621      0.566 0.008 0.284 0.000 0.708
#&gt; SRR1975491     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975492     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975489     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975487     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975488     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975485     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975486     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975483     4  0.0336      0.969 0.008 0.000 0.000 0.992
#&gt; SRR1975484     4  0.0336      0.969 0.008 0.000 0.000 0.992
#&gt; SRR1975481     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975482     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975477     2  0.0000      0.927 0.000 1.000 0.000 0.000
#&gt; SRR1975478     2  0.0000      0.927 0.000 1.000 0.000 0.000
#&gt; SRR1975479     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975480     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975475     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975476     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975473     2  0.0188      0.925 0.004 0.996 0.000 0.000
#&gt; SRR1975474     2  0.0188      0.925 0.004 0.996 0.000 0.000
#&gt; SRR1975471     2  0.4328      0.494 0.008 0.748 0.000 0.244
#&gt; SRR1975472     2  0.4328      0.494 0.008 0.748 0.000 0.244
#&gt; SRR1975469     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975470     4  0.0000      0.975 0.000 0.000 0.000 1.000
#&gt; SRR1975467     4  0.0188      0.972 0.004 0.000 0.000 0.996
#&gt; SRR1975468     4  0.0188      0.972 0.004 0.000 0.000 0.996
#&gt; SRR1975465     2  0.0000      0.927 0.000 1.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.927 0.000 1.000 0.000 0.000
#&gt; SRR1975463     2  0.0469      0.921 0.012 0.988 0.000 0.000
#&gt; SRR1975464     2  0.0469      0.921 0.012 0.988 0.000 0.000
#&gt; SRR1975461     1  0.0469      0.398 0.988 0.000 0.012 0.000
#&gt; SRR1975462     1  0.0469      0.398 0.988 0.000 0.012 0.000
#&gt; SRR1975459     2  0.0000      0.927 0.000 1.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.927 0.000 1.000 0.000 0.000
#&gt; SRR1975457     2  0.0000      0.927 0.000 1.000 0.000 0.000
#&gt; SRR1975458     2  0.0000      0.927 0.000 1.000 0.000 0.000
#&gt; SRR1975455     2  0.0000      0.927 0.000 1.000 0.000 0.000
#&gt; SRR1975456     2  0.0000      0.927 0.000 1.000 0.000 0.000
#&gt; SRR1975453     1  0.4999      0.342 0.508 0.492 0.000 0.000
#&gt; SRR1975454     1  0.4999      0.342 0.508 0.492 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-3-a').click(function(){
  $('#tab-ATC-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-4'>
<p><a id='tab-ATC-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1975503     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975504     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975501     4  0.1965      0.906 0.000 0.096  0 0.904 0.000
#&gt; SRR1975502     4  0.1965      0.906 0.000 0.096  0 0.904 0.000
#&gt; SRR1975499     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975500     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975497     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975498     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975493     2  0.3774      0.544 0.000 0.704  0 0.000 0.296
#&gt; SRR1975494     2  0.3774      0.544 0.000 0.704  0 0.000 0.296
#&gt; SRR1975495     2  0.4297     -0.226 0.000 0.528  0 0.472 0.000
#&gt; SRR1975496     2  0.4297     -0.226 0.000 0.528  0 0.472 0.000
#&gt; SRR1975491     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975492     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975489     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975490     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975487     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975488     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975485     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975486     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975483     4  0.3109      0.819 0.000 0.200  0 0.800 0.000
#&gt; SRR1975484     4  0.3109      0.819 0.000 0.200  0 0.800 0.000
#&gt; SRR1975481     4  0.2561      0.873 0.000 0.144  0 0.856 0.000
#&gt; SRR1975482     4  0.2561      0.873 0.000 0.144  0 0.856 0.000
#&gt; SRR1975477     5  0.0000      0.994 0.000 0.000  0 0.000 1.000
#&gt; SRR1975478     5  0.0000      0.994 0.000 0.000  0 0.000 1.000
#&gt; SRR1975479     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975480     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975475     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975476     4  0.0000      0.955 0.000 0.000  0 1.000 0.000
#&gt; SRR1975473     5  0.0404      0.983 0.000 0.012  0 0.000 0.988
#&gt; SRR1975474     5  0.0404      0.983 0.000 0.012  0 0.000 0.988
#&gt; SRR1975471     2  0.4542     -0.198 0.000 0.536  0 0.008 0.456
#&gt; SRR1975472     2  0.4542     -0.198 0.000 0.536  0 0.008 0.456
#&gt; SRR1975469     4  0.2424      0.882 0.000 0.132  0 0.868 0.000
#&gt; SRR1975470     4  0.2424      0.882 0.000 0.132  0 0.868 0.000
#&gt; SRR1975467     4  0.0794      0.941 0.000 0.028  0 0.972 0.000
#&gt; SRR1975468     4  0.0794      0.941 0.000 0.028  0 0.972 0.000
#&gt; SRR1975465     2  0.4045      0.541 0.000 0.644  0 0.000 0.356
#&gt; SRR1975466     2  0.4045      0.541 0.000 0.644  0 0.000 0.356
#&gt; SRR1975463     2  0.3966      0.546 0.000 0.664  0 0.000 0.336
#&gt; SRR1975464     2  0.3966      0.546 0.000 0.664  0 0.000 0.336
#&gt; SRR1975461     1  0.0000      0.525 1.000 0.000  0 0.000 0.000
#&gt; SRR1975462     1  0.0000      0.525 1.000 0.000  0 0.000 0.000
#&gt; SRR1975459     2  0.4045      0.541 0.000 0.644  0 0.000 0.356
#&gt; SRR1975460     2  0.4045      0.541 0.000 0.644  0 0.000 0.356
#&gt; SRR1975457     5  0.0000      0.994 0.000 0.000  0 0.000 1.000
#&gt; SRR1975458     5  0.0000      0.994 0.000 0.000  0 0.000 1.000
#&gt; SRR1975455     5  0.0000      0.994 0.000 0.000  0 0.000 1.000
#&gt; SRR1975456     5  0.0000      0.994 0.000 0.000  0 0.000 1.000
#&gt; SRR1975453     1  0.4306      0.383 0.508 0.000  0 0.000 0.492
#&gt; SRR1975454     1  0.4306      0.383 0.508 0.000  0 0.000 0.492
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-4-a').click(function(){
  $('#tab-ATC-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-5'>
<p><a id='tab-ATC-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5    p6
#&gt; SRR1975508     3  0.0000     1.0000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975507     3  0.0000     1.0000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975506     3  0.0000     1.0000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975505     3  0.0000     1.0000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975503     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975504     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975501     4  0.1765     0.8667 0.096 0.000  0 0.904 0.000 0.000
#&gt; SRR1975502     4  0.1765     0.8667 0.096 0.000  0 0.904 0.000 0.000
#&gt; SRR1975499     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975500     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975497     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975498     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975493     2  0.1501     0.9412 0.076 0.924  0 0.000 0.000 0.000
#&gt; SRR1975494     2  0.1501     0.9412 0.076 0.924  0 0.000 0.000 0.000
#&gt; SRR1975495     1  0.3854     0.2916 0.536 0.000  0 0.464 0.000 0.000
#&gt; SRR1975496     1  0.3854     0.2916 0.536 0.000  0 0.464 0.000 0.000
#&gt; SRR1975491     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975492     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975489     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975490     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975487     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975488     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975485     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975486     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975483     4  0.2854     0.7179 0.208 0.000  0 0.792 0.000 0.000
#&gt; SRR1975484     4  0.2854     0.7179 0.208 0.000  0 0.792 0.000 0.000
#&gt; SRR1975481     4  0.2340     0.8127 0.148 0.000  0 0.852 0.000 0.000
#&gt; SRR1975482     4  0.2340     0.8127 0.148 0.000  0 0.852 0.000 0.000
#&gt; SRR1975477     5  0.0000     0.9959 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975478     5  0.0000     0.9959 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975479     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975480     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975475     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975476     4  0.0000     0.9377 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975473     5  0.0405     0.9876 0.008 0.004  0 0.000 0.988 0.000
#&gt; SRR1975474     5  0.0405     0.9876 0.008 0.004  0 0.000 0.988 0.000
#&gt; SRR1975471     1  0.0713     0.0414 0.972 0.000  0 0.000 0.028 0.000
#&gt; SRR1975472     1  0.0713     0.0414 0.972 0.000  0 0.000 0.028 0.000
#&gt; SRR1975469     4  0.2219     0.8267 0.136 0.000  0 0.864 0.000 0.000
#&gt; SRR1975470     4  0.2219     0.8267 0.136 0.000  0 0.864 0.000 0.000
#&gt; SRR1975467     4  0.0820     0.9187 0.016 0.012  0 0.972 0.000 0.000
#&gt; SRR1975468     4  0.0820     0.9187 0.016 0.012  0 0.972 0.000 0.000
#&gt; SRR1975465     2  0.0547     0.9665 0.000 0.980  0 0.000 0.020 0.000
#&gt; SRR1975466     2  0.0547     0.9665 0.000 0.980  0 0.000 0.020 0.000
#&gt; SRR1975463     2  0.1391     0.9630 0.040 0.944  0 0.000 0.016 0.000
#&gt; SRR1975464     2  0.1391     0.9630 0.040 0.944  0 0.000 0.016 0.000
#&gt; SRR1975461     6  0.0000     0.6878 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1975462     6  0.0000     0.6878 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1975459     2  0.0547     0.9665 0.000 0.980  0 0.000 0.020 0.000
#&gt; SRR1975460     2  0.0547     0.9665 0.000 0.980  0 0.000 0.020 0.000
#&gt; SRR1975457     5  0.0000     0.9959 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975458     5  0.0000     0.9959 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975455     5  0.0000     0.9959 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975456     5  0.0000     0.9959 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975453     6  0.5112     0.6824 0.428 0.008  0 0.000 0.060 0.504
#&gt; SRR1975454     6  0.5112     0.6824 0.428 0.008  0 0.000 0.060 0.504
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-5-a').click(function(){
  $('#tab-ATC-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-hclust-signature_compare](figure_cola/ATC-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-hclust-collect-classes](figure_cola/ATC-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "kmeans"]
# you can also extract it by
# res = res_list["ATC:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-kmeans-collect-plots](figure_cola/ATC-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-kmeans-select-partition-number](figure_cola/ATC-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.539           0.896       0.939         0.4352 0.532   0.532
#> 3 3 0.670           0.767       0.840         0.4108 0.774   0.615
#> 4 4 0.620           0.653       0.784         0.1311 0.852   0.652
#> 5 5 0.606           0.660       0.777         0.0885 0.927   0.769
#> 6 6 0.645           0.543       0.702         0.0512 0.953   0.825
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-kmeans-get-classes-1'>
<p><a id='tab-ATC-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2   0.000      0.863 0.000 1.000
#&gt; SRR1975507     2   0.000      0.863 0.000 1.000
#&gt; SRR1975506     2   0.000      0.863 0.000 1.000
#&gt; SRR1975505     2   0.000      0.863 0.000 1.000
#&gt; SRR1975503     1   0.000      0.964 1.000 0.000
#&gt; SRR1975504     1   0.000      0.964 1.000 0.000
#&gt; SRR1975501     1   0.000      0.964 1.000 0.000
#&gt; SRR1975502     1   0.000      0.964 1.000 0.000
#&gt; SRR1975499     1   0.000      0.964 1.000 0.000
#&gt; SRR1975500     1   0.000      0.964 1.000 0.000
#&gt; SRR1975497     1   0.000      0.964 1.000 0.000
#&gt; SRR1975498     1   0.000      0.964 1.000 0.000
#&gt; SRR1975493     1   0.000      0.964 1.000 0.000
#&gt; SRR1975494     1   0.000      0.964 1.000 0.000
#&gt; SRR1975495     1   0.000      0.964 1.000 0.000
#&gt; SRR1975496     1   0.000      0.964 1.000 0.000
#&gt; SRR1975491     1   0.000      0.964 1.000 0.000
#&gt; SRR1975492     1   0.000      0.964 1.000 0.000
#&gt; SRR1975489     1   0.000      0.964 1.000 0.000
#&gt; SRR1975490     1   0.000      0.964 1.000 0.000
#&gt; SRR1975487     1   0.000      0.964 1.000 0.000
#&gt; SRR1975488     1   0.000      0.964 1.000 0.000
#&gt; SRR1975485     1   0.000      0.964 1.000 0.000
#&gt; SRR1975486     1   0.000      0.964 1.000 0.000
#&gt; SRR1975483     1   0.000      0.964 1.000 0.000
#&gt; SRR1975484     1   0.000      0.964 1.000 0.000
#&gt; SRR1975481     1   0.000      0.964 1.000 0.000
#&gt; SRR1975482     1   0.000      0.964 1.000 0.000
#&gt; SRR1975477     2   0.552      0.913 0.128 0.872
#&gt; SRR1975478     2   0.552      0.913 0.128 0.872
#&gt; SRR1975479     1   0.000      0.964 1.000 0.000
#&gt; SRR1975480     1   0.000      0.964 1.000 0.000
#&gt; SRR1975475     1   0.000      0.964 1.000 0.000
#&gt; SRR1975476     1   0.000      0.964 1.000 0.000
#&gt; SRR1975473     1   0.921      0.406 0.664 0.336
#&gt; SRR1975474     1   0.921      0.406 0.664 0.336
#&gt; SRR1975471     1   0.689      0.733 0.816 0.184
#&gt; SRR1975472     1   0.689      0.733 0.816 0.184
#&gt; SRR1975469     1   0.000      0.964 1.000 0.000
#&gt; SRR1975470     1   0.000      0.964 1.000 0.000
#&gt; SRR1975467     1   0.000      0.964 1.000 0.000
#&gt; SRR1975468     1   0.000      0.964 1.000 0.000
#&gt; SRR1975465     2   0.552      0.913 0.128 0.872
#&gt; SRR1975466     2   0.552      0.913 0.128 0.872
#&gt; SRR1975463     2   0.978      0.451 0.412 0.588
#&gt; SRR1975464     2   0.978      0.451 0.412 0.588
#&gt; SRR1975461     2   0.000      0.863 0.000 1.000
#&gt; SRR1975462     2   0.000      0.863 0.000 1.000
#&gt; SRR1975459     2   0.552      0.913 0.128 0.872
#&gt; SRR1975460     2   0.552      0.913 0.128 0.872
#&gt; SRR1975457     2   0.552      0.913 0.128 0.872
#&gt; SRR1975458     2   0.552      0.913 0.128 0.872
#&gt; SRR1975455     2   0.552      0.913 0.128 0.872
#&gt; SRR1975456     2   0.552      0.913 0.128 0.872
#&gt; SRR1975453     2   0.552      0.913 0.128 0.872
#&gt; SRR1975454     2   0.552      0.913 0.128 0.872
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-2'>
<p><a id='tab-ATC-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.0592      0.925 0.000 0.012 0.988
#&gt; SRR1975507     3  0.0592      0.925 0.000 0.012 0.988
#&gt; SRR1975506     3  0.0592      0.925 0.000 0.012 0.988
#&gt; SRR1975505     3  0.0592      0.925 0.000 0.012 0.988
#&gt; SRR1975503     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975504     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975501     1  0.2878      0.847 0.904 0.096 0.000
#&gt; SRR1975502     1  0.2878      0.847 0.904 0.096 0.000
#&gt; SRR1975499     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975500     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975497     1  0.0237      0.851 0.996 0.004 0.000
#&gt; SRR1975498     1  0.0237      0.851 0.996 0.004 0.000
#&gt; SRR1975493     2  0.1643      0.590 0.044 0.956 0.000
#&gt; SRR1975494     2  0.1643      0.590 0.044 0.956 0.000
#&gt; SRR1975495     1  0.6189      0.743 0.632 0.364 0.004
#&gt; SRR1975496     1  0.6189      0.743 0.632 0.364 0.004
#&gt; SRR1975491     1  0.5138      0.807 0.748 0.252 0.000
#&gt; SRR1975492     1  0.5138      0.807 0.748 0.252 0.000
#&gt; SRR1975489     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975490     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975487     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975488     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975485     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975486     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975483     1  0.5968      0.746 0.636 0.364 0.000
#&gt; SRR1975484     1  0.5968      0.746 0.636 0.364 0.000
#&gt; SRR1975481     1  0.5968      0.746 0.636 0.364 0.000
#&gt; SRR1975482     1  0.5968      0.746 0.636 0.364 0.000
#&gt; SRR1975477     2  0.5968      0.674 0.000 0.636 0.364
#&gt; SRR1975478     2  0.5968      0.674 0.000 0.636 0.364
#&gt; SRR1975479     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975480     1  0.0000      0.852 1.000 0.000 0.000
#&gt; SRR1975475     1  0.1860      0.852 0.948 0.052 0.000
#&gt; SRR1975476     1  0.1860      0.852 0.948 0.052 0.000
#&gt; SRR1975473     2  0.0237      0.628 0.004 0.996 0.000
#&gt; SRR1975474     2  0.0237      0.628 0.004 0.996 0.000
#&gt; SRR1975471     2  0.0829      0.620 0.004 0.984 0.012
#&gt; SRR1975472     2  0.0829      0.620 0.004 0.984 0.012
#&gt; SRR1975469     1  0.5431      0.795 0.716 0.284 0.000
#&gt; SRR1975470     1  0.5431      0.795 0.716 0.284 0.000
#&gt; SRR1975467     1  0.5591      0.784 0.696 0.304 0.000
#&gt; SRR1975468     1  0.5591      0.784 0.696 0.304 0.000
#&gt; SRR1975465     2  0.5948      0.675 0.000 0.640 0.360
#&gt; SRR1975466     2  0.5948      0.675 0.000 0.640 0.360
#&gt; SRR1975463     2  0.0237      0.628 0.004 0.996 0.000
#&gt; SRR1975464     2  0.0237      0.628 0.004 0.996 0.000
#&gt; SRR1975461     3  0.3482      0.826 0.000 0.128 0.872
#&gt; SRR1975462     3  0.3482      0.826 0.000 0.128 0.872
#&gt; SRR1975459     2  0.5968      0.674 0.000 0.636 0.364
#&gt; SRR1975460     2  0.5968      0.674 0.000 0.636 0.364
#&gt; SRR1975457     2  0.5968      0.674 0.000 0.636 0.364
#&gt; SRR1975458     2  0.5968      0.674 0.000 0.636 0.364
#&gt; SRR1975455     2  0.5968      0.674 0.000 0.636 0.364
#&gt; SRR1975456     2  0.5968      0.674 0.000 0.636 0.364
#&gt; SRR1975453     2  0.5905      0.671 0.000 0.648 0.352
#&gt; SRR1975454     2  0.5905      0.671 0.000 0.648 0.352
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-3'>
<p><a id='tab-ATC-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.1940     0.8959 0.000 0.076 0.924 0.000
#&gt; SRR1975507     3  0.1940     0.8959 0.000 0.076 0.924 0.000
#&gt; SRR1975506     3  0.2125     0.8959 0.004 0.076 0.920 0.000
#&gt; SRR1975505     3  0.2125     0.8959 0.004 0.076 0.920 0.000
#&gt; SRR1975503     4  0.0524     0.8003 0.004 0.000 0.008 0.988
#&gt; SRR1975504     4  0.0524     0.8003 0.004 0.000 0.008 0.988
#&gt; SRR1975501     4  0.4718     0.4456 0.280 0.000 0.012 0.708
#&gt; SRR1975502     4  0.4718     0.4456 0.280 0.000 0.012 0.708
#&gt; SRR1975499     4  0.0188     0.8030 0.000 0.000 0.004 0.996
#&gt; SRR1975500     4  0.0188     0.8030 0.000 0.000 0.004 0.996
#&gt; SRR1975497     4  0.0804     0.7993 0.012 0.000 0.008 0.980
#&gt; SRR1975498     4  0.0804     0.7993 0.012 0.000 0.008 0.980
#&gt; SRR1975493     2  0.5819     0.5017 0.404 0.568 0.012 0.016
#&gt; SRR1975494     2  0.5819     0.5017 0.404 0.568 0.012 0.016
#&gt; SRR1975495     1  0.4406     0.6991 0.700 0.000 0.000 0.300
#&gt; SRR1975496     1  0.4406     0.6991 0.700 0.000 0.000 0.300
#&gt; SRR1975491     4  0.5300     0.0444 0.408 0.000 0.012 0.580
#&gt; SRR1975492     4  0.5300     0.0444 0.408 0.000 0.012 0.580
#&gt; SRR1975489     4  0.0469     0.8017 0.000 0.000 0.012 0.988
#&gt; SRR1975490     4  0.0469     0.8017 0.000 0.000 0.012 0.988
#&gt; SRR1975487     4  0.0188     0.8030 0.000 0.000 0.004 0.996
#&gt; SRR1975488     4  0.0188     0.8030 0.000 0.000 0.004 0.996
#&gt; SRR1975485     4  0.0188     0.8030 0.000 0.000 0.004 0.996
#&gt; SRR1975486     4  0.0188     0.8030 0.000 0.000 0.004 0.996
#&gt; SRR1975483     1  0.4522     0.7007 0.680 0.000 0.000 0.320
#&gt; SRR1975484     1  0.4522     0.7007 0.680 0.000 0.000 0.320
#&gt; SRR1975481     1  0.4605     0.6885 0.664 0.000 0.000 0.336
#&gt; SRR1975482     1  0.4605     0.6885 0.664 0.000 0.000 0.336
#&gt; SRR1975477     2  0.0469     0.8041 0.012 0.988 0.000 0.000
#&gt; SRR1975478     2  0.0469     0.8041 0.012 0.988 0.000 0.000
#&gt; SRR1975479     4  0.1545     0.7866 0.008 0.000 0.040 0.952
#&gt; SRR1975480     4  0.1545     0.7866 0.008 0.000 0.040 0.952
#&gt; SRR1975475     4  0.4050     0.6821 0.144 0.000 0.036 0.820
#&gt; SRR1975476     4  0.4050     0.6821 0.144 0.000 0.036 0.820
#&gt; SRR1975473     2  0.3486     0.7551 0.188 0.812 0.000 0.000
#&gt; SRR1975474     2  0.3486     0.7551 0.188 0.812 0.000 0.000
#&gt; SRR1975471     1  0.4836     0.0110 0.672 0.320 0.008 0.000
#&gt; SRR1975472     1  0.4836     0.0110 0.672 0.320 0.008 0.000
#&gt; SRR1975469     1  0.5290     0.3643 0.516 0.000 0.008 0.476
#&gt; SRR1975470     1  0.5290     0.3643 0.516 0.000 0.008 0.476
#&gt; SRR1975467     4  0.5483    -0.0296 0.448 0.000 0.016 0.536
#&gt; SRR1975468     4  0.5483    -0.0296 0.448 0.000 0.016 0.536
#&gt; SRR1975465     2  0.2011     0.7982 0.080 0.920 0.000 0.000
#&gt; SRR1975466     2  0.2011     0.7982 0.080 0.920 0.000 0.000
#&gt; SRR1975463     2  0.3751     0.7688 0.196 0.800 0.004 0.000
#&gt; SRR1975464     2  0.3751     0.7688 0.196 0.800 0.004 0.000
#&gt; SRR1975461     3  0.6327     0.7536 0.132 0.216 0.652 0.000
#&gt; SRR1975462     3  0.6327     0.7536 0.132 0.216 0.652 0.000
#&gt; SRR1975459     2  0.2011     0.7969 0.080 0.920 0.000 0.000
#&gt; SRR1975460     2  0.2011     0.7969 0.080 0.920 0.000 0.000
#&gt; SRR1975457     2  0.2011     0.7895 0.080 0.920 0.000 0.000
#&gt; SRR1975458     2  0.2011     0.7895 0.080 0.920 0.000 0.000
#&gt; SRR1975455     2  0.1940     0.7910 0.076 0.924 0.000 0.000
#&gt; SRR1975456     2  0.1940     0.7910 0.076 0.924 0.000 0.000
#&gt; SRR1975453     2  0.5110     0.5435 0.352 0.636 0.012 0.000
#&gt; SRR1975454     2  0.5110     0.5435 0.352 0.636 0.012 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-4'>
<p><a id='tab-ATC-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR1975508     3  0.0404      0.859 0.000 0.012 0.988 0.000 NA
#&gt; SRR1975507     3  0.0404      0.859 0.000 0.012 0.988 0.000 NA
#&gt; SRR1975506     3  0.1095      0.859 0.012 0.012 0.968 0.000 NA
#&gt; SRR1975505     3  0.1095      0.859 0.012 0.012 0.968 0.000 NA
#&gt; SRR1975503     4  0.1991      0.823 0.004 0.000 0.004 0.916 NA
#&gt; SRR1975504     4  0.1991      0.823 0.004 0.000 0.004 0.916 NA
#&gt; SRR1975501     4  0.6142      0.047 0.352 0.000 0.004 0.520 NA
#&gt; SRR1975502     4  0.6142      0.047 0.352 0.000 0.004 0.520 NA
#&gt; SRR1975499     4  0.0162      0.837 0.000 0.000 0.004 0.996 NA
#&gt; SRR1975500     4  0.0162      0.837 0.000 0.000 0.004 0.996 NA
#&gt; SRR1975497     4  0.2484      0.808 0.028 0.000 0.004 0.900 NA
#&gt; SRR1975498     4  0.2484      0.808 0.028 0.000 0.004 0.900 NA
#&gt; SRR1975493     2  0.6035      0.450 0.204 0.580 0.000 0.000 NA
#&gt; SRR1975494     2  0.6035      0.450 0.204 0.580 0.000 0.000 NA
#&gt; SRR1975495     1  0.3012      0.711 0.852 0.000 0.000 0.124 NA
#&gt; SRR1975496     1  0.3012      0.711 0.852 0.000 0.000 0.124 NA
#&gt; SRR1975491     1  0.6845      0.339 0.400 0.000 0.004 0.348 NA
#&gt; SRR1975492     1  0.6845      0.339 0.400 0.000 0.004 0.348 NA
#&gt; SRR1975489     4  0.0609      0.835 0.000 0.000 0.000 0.980 NA
#&gt; SRR1975490     4  0.0609      0.835 0.000 0.000 0.000 0.980 NA
#&gt; SRR1975487     4  0.0290      0.836 0.000 0.000 0.000 0.992 NA
#&gt; SRR1975488     4  0.0290      0.836 0.000 0.000 0.000 0.992 NA
#&gt; SRR1975485     4  0.0000      0.836 0.000 0.000 0.000 1.000 NA
#&gt; SRR1975486     4  0.0000      0.836 0.000 0.000 0.000 1.000 NA
#&gt; SRR1975483     1  0.2969      0.712 0.852 0.000 0.000 0.128 NA
#&gt; SRR1975484     1  0.2969      0.712 0.852 0.000 0.000 0.128 NA
#&gt; SRR1975481     1  0.3521      0.713 0.820 0.000 0.000 0.140 NA
#&gt; SRR1975482     1  0.3521      0.713 0.820 0.000 0.000 0.140 NA
#&gt; SRR1975477     2  0.3282      0.751 0.008 0.804 0.000 0.000 NA
#&gt; SRR1975478     2  0.3282      0.751 0.008 0.804 0.000 0.000 NA
#&gt; SRR1975479     4  0.2694      0.801 0.004 0.000 0.004 0.864 NA
#&gt; SRR1975480     4  0.2694      0.801 0.004 0.000 0.004 0.864 NA
#&gt; SRR1975475     4  0.5909      0.447 0.164 0.000 0.000 0.592 NA
#&gt; SRR1975476     4  0.5909      0.447 0.164 0.000 0.000 0.592 NA
#&gt; SRR1975473     2  0.5039      0.724 0.080 0.676 0.000 0.000 NA
#&gt; SRR1975474     2  0.5039      0.724 0.080 0.676 0.000 0.000 NA
#&gt; SRR1975471     1  0.4595      0.417 0.740 0.088 0.000 0.000 NA
#&gt; SRR1975472     1  0.4595      0.417 0.740 0.088 0.000 0.000 NA
#&gt; SRR1975469     1  0.5533      0.612 0.640 0.000 0.004 0.252 NA
#&gt; SRR1975470     1  0.5533      0.612 0.640 0.000 0.004 0.252 NA
#&gt; SRR1975467     1  0.6795      0.352 0.364 0.000 0.000 0.288 NA
#&gt; SRR1975468     1  0.6795      0.352 0.364 0.000 0.000 0.288 NA
#&gt; SRR1975465     2  0.0771      0.738 0.004 0.976 0.000 0.000 NA
#&gt; SRR1975466     2  0.0771      0.738 0.004 0.976 0.000 0.000 NA
#&gt; SRR1975463     2  0.2514      0.716 0.044 0.896 0.000 0.000 NA
#&gt; SRR1975464     2  0.2514      0.716 0.044 0.896 0.000 0.000 NA
#&gt; SRR1975461     3  0.6666      0.665 0.036 0.164 0.572 0.000 NA
#&gt; SRR1975462     3  0.6666      0.665 0.036 0.164 0.572 0.000 NA
#&gt; SRR1975459     2  0.0771      0.737 0.004 0.976 0.000 0.000 NA
#&gt; SRR1975460     2  0.0771      0.737 0.004 0.976 0.000 0.000 NA
#&gt; SRR1975457     2  0.4090      0.730 0.016 0.716 0.000 0.000 NA
#&gt; SRR1975458     2  0.4090      0.730 0.016 0.716 0.000 0.000 NA
#&gt; SRR1975455     2  0.4065      0.732 0.016 0.720 0.000 0.000 NA
#&gt; SRR1975456     2  0.4065      0.732 0.016 0.720 0.000 0.000 NA
#&gt; SRR1975453     2  0.6609      0.404 0.216 0.416 0.000 0.000 NA
#&gt; SRR1975454     2  0.6609      0.404 0.216 0.416 0.000 0.000 NA
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-5'>
<p><a id='tab-ATC-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     3  0.0146     0.8024 0.000 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1975507     3  0.0146     0.8024 0.000 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1975506     3  0.0653     0.8024 0.000 0.004 0.980 0.000 0.004 0.012
#&gt; SRR1975505     3  0.0653     0.8024 0.000 0.004 0.980 0.000 0.004 0.012
#&gt; SRR1975503     4  0.3660     0.6672 0.004 0.036 0.000 0.772 0.000 0.188
#&gt; SRR1975504     4  0.3660     0.6672 0.004 0.036 0.000 0.772 0.000 0.188
#&gt; SRR1975501     4  0.6839    -0.3034 0.320 0.060 0.000 0.412 0.000 0.208
#&gt; SRR1975502     4  0.6839    -0.3034 0.320 0.060 0.000 0.412 0.000 0.208
#&gt; SRR1975499     4  0.0363     0.7565 0.000 0.012 0.000 0.988 0.000 0.000
#&gt; SRR1975500     4  0.0363     0.7565 0.000 0.012 0.000 0.988 0.000 0.000
#&gt; SRR1975497     4  0.3238     0.7071 0.024 0.056 0.000 0.848 0.000 0.072
#&gt; SRR1975498     4  0.3238     0.7071 0.024 0.056 0.000 0.848 0.000 0.072
#&gt; SRR1975493     2  0.7375     1.0000 0.112 0.340 0.000 0.000 0.272 0.276
#&gt; SRR1975494     2  0.7375     1.0000 0.112 0.340 0.000 0.000 0.272 0.276
#&gt; SRR1975495     1  0.2555     0.6890 0.888 0.016 0.000 0.064 0.000 0.032
#&gt; SRR1975496     1  0.2555     0.6890 0.888 0.016 0.000 0.064 0.000 0.032
#&gt; SRR1975491     6  0.6648     0.6562 0.360 0.044 0.000 0.196 0.000 0.400
#&gt; SRR1975492     6  0.6648     0.6562 0.360 0.044 0.000 0.196 0.000 0.400
#&gt; SRR1975489     4  0.0806     0.7545 0.000 0.020 0.000 0.972 0.000 0.008
#&gt; SRR1975490     4  0.0806     0.7545 0.000 0.020 0.000 0.972 0.000 0.008
#&gt; SRR1975487     4  0.0508     0.7558 0.000 0.012 0.000 0.984 0.000 0.004
#&gt; SRR1975488     4  0.0508     0.7558 0.000 0.012 0.000 0.984 0.000 0.004
#&gt; SRR1975485     4  0.0000     0.7557 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975486     4  0.0000     0.7557 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975483     1  0.2953     0.6888 0.864 0.040 0.000 0.076 0.000 0.020
#&gt; SRR1975484     1  0.2953     0.6888 0.864 0.040 0.000 0.076 0.000 0.020
#&gt; SRR1975481     1  0.3457     0.6524 0.832 0.024 0.000 0.084 0.000 0.060
#&gt; SRR1975482     1  0.3457     0.6524 0.832 0.024 0.000 0.084 0.000 0.060
#&gt; SRR1975477     5  0.1408     0.5491 0.000 0.036 0.000 0.000 0.944 0.020
#&gt; SRR1975478     5  0.1408     0.5491 0.000 0.036 0.000 0.000 0.944 0.020
#&gt; SRR1975479     4  0.4044     0.6547 0.008 0.060 0.000 0.756 0.000 0.176
#&gt; SRR1975480     4  0.4044     0.6547 0.008 0.060 0.000 0.756 0.000 0.176
#&gt; SRR1975475     4  0.5925     0.0968 0.100 0.032 0.000 0.472 0.000 0.396
#&gt; SRR1975476     4  0.5925     0.0968 0.100 0.032 0.000 0.472 0.000 0.396
#&gt; SRR1975473     5  0.4327     0.3751 0.048 0.108 0.000 0.000 0.772 0.072
#&gt; SRR1975474     5  0.4327     0.3751 0.048 0.108 0.000 0.000 0.772 0.072
#&gt; SRR1975471     1  0.4837     0.4837 0.724 0.112 0.000 0.000 0.124 0.040
#&gt; SRR1975472     1  0.4837     0.4837 0.724 0.112 0.000 0.000 0.124 0.040
#&gt; SRR1975469     1  0.5908     0.2871 0.628 0.060 0.004 0.164 0.000 0.144
#&gt; SRR1975470     1  0.5908     0.2871 0.628 0.060 0.004 0.164 0.000 0.144
#&gt; SRR1975467     6  0.5919     0.7126 0.220 0.040 0.000 0.152 0.000 0.588
#&gt; SRR1975468     6  0.5919     0.7126 0.220 0.040 0.000 0.152 0.000 0.588
#&gt; SRR1975465     5  0.3881     0.3565 0.000 0.396 0.000 0.000 0.600 0.004
#&gt; SRR1975466     5  0.3881     0.3565 0.000 0.396 0.000 0.000 0.600 0.004
#&gt; SRR1975463     5  0.4713     0.2137 0.012 0.400 0.000 0.000 0.560 0.028
#&gt; SRR1975464     5  0.4713     0.2137 0.012 0.400 0.000 0.000 0.560 0.028
#&gt; SRR1975461     3  0.7244     0.5487 0.028 0.264 0.476 0.000 0.144 0.088
#&gt; SRR1975462     3  0.7244     0.5487 0.028 0.264 0.476 0.000 0.144 0.088
#&gt; SRR1975459     5  0.4063     0.3418 0.004 0.420 0.000 0.000 0.572 0.004
#&gt; SRR1975460     5  0.4063     0.3418 0.004 0.420 0.000 0.000 0.572 0.004
#&gt; SRR1975457     5  0.1225     0.5460 0.000 0.036 0.000 0.000 0.952 0.012
#&gt; SRR1975458     5  0.1225     0.5460 0.000 0.036 0.000 0.000 0.952 0.012
#&gt; SRR1975455     5  0.1168     0.5488 0.000 0.028 0.000 0.000 0.956 0.016
#&gt; SRR1975456     5  0.1168     0.5488 0.000 0.028 0.000 0.000 0.956 0.016
#&gt; SRR1975453     5  0.6951     0.1171 0.240 0.260 0.000 0.000 0.428 0.072
#&gt; SRR1975454     5  0.6951     0.1171 0.240 0.260 0.000 0.000 0.428 0.072
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-kmeans-signature_compare](figure_cola/ATC-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-kmeans-collect-classes](figure_cola/ATC-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "skmeans"]
# you can also extract it by
# res = res_list["ATC:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-skmeans-collect-plots](figure_cola/ATC-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-skmeans-select-partition-number](figure_cola/ATC-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.955       0.983         0.5026 0.501   0.501
#> 3 3 0.762           0.884       0.911         0.2080 0.883   0.770
#> 4 4 0.821           0.880       0.905         0.1320 0.878   0.701
#> 5 5 0.765           0.716       0.851         0.0705 0.982   0.938
#> 6 6 0.723           0.646       0.785         0.0420 0.974   0.907
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-skmeans-get-classes-1'>
<p><a id='tab-ATC-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975507     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975506     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975505     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975503     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975504     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975501     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975502     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975499     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975500     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975497     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975498     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975493     1  0.9933      0.202 0.548 0.452
#&gt; SRR1975494     1  0.9933      0.202 0.548 0.452
#&gt; SRR1975495     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975496     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975491     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975492     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975489     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975490     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975487     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975488     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975485     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975486     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975483     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975484     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975481     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975482     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975477     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975478     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975479     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975480     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975475     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975476     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975473     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975474     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975471     2  0.0938      0.988 0.012 0.988
#&gt; SRR1975472     2  0.0938      0.988 0.012 0.988
#&gt; SRR1975469     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975470     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975467     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975468     1  0.0000      0.970 1.000 0.000
#&gt; SRR1975465     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975466     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975463     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975464     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975461     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975462     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975459     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975460     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975457     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975458     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975455     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975456     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975453     2  0.0000      0.999 0.000 1.000
#&gt; SRR1975454     2  0.0000      0.999 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-2'>
<p><a id='tab-ATC-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.0000      0.894 0.000 0.000 1.000
#&gt; SRR1975507     3  0.0000      0.894 0.000 0.000 1.000
#&gt; SRR1975506     3  0.0000      0.894 0.000 0.000 1.000
#&gt; SRR1975505     3  0.0000      0.894 0.000 0.000 1.000
#&gt; SRR1975503     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975504     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975501     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975502     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975499     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975500     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975497     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975493     2  0.6299      0.776 0.096 0.772 0.132
#&gt; SRR1975494     2  0.6299      0.776 0.096 0.772 0.132
#&gt; SRR1975495     1  0.4974      0.787 0.764 0.236 0.000
#&gt; SRR1975496     1  0.4974      0.787 0.764 0.236 0.000
#&gt; SRR1975491     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975492     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975489     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975490     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975487     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975488     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975485     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975486     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975483     1  0.4887      0.794 0.772 0.228 0.000
#&gt; SRR1975484     1  0.4887      0.794 0.772 0.228 0.000
#&gt; SRR1975481     1  0.4291      0.835 0.820 0.180 0.000
#&gt; SRR1975482     1  0.4291      0.835 0.820 0.180 0.000
#&gt; SRR1975477     3  0.0237      0.891 0.000 0.004 0.996
#&gt; SRR1975478     3  0.0237      0.891 0.000 0.004 0.996
#&gt; SRR1975479     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975480     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975475     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975476     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975473     3  0.4291      0.727 0.000 0.180 0.820
#&gt; SRR1975474     3  0.4291      0.727 0.000 0.180 0.820
#&gt; SRR1975471     3  0.5785      0.599 0.000 0.332 0.668
#&gt; SRR1975472     3  0.5785      0.599 0.000 0.332 0.668
#&gt; SRR1975469     1  0.0592      0.950 0.988 0.012 0.000
#&gt; SRR1975470     1  0.0592      0.950 0.988 0.012 0.000
#&gt; SRR1975467     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975468     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1975465     2  0.5835      0.878 0.000 0.660 0.340
#&gt; SRR1975466     2  0.5835      0.878 0.000 0.660 0.340
#&gt; SRR1975463     2  0.5363      0.875 0.000 0.724 0.276
#&gt; SRR1975464     2  0.5363      0.875 0.000 0.724 0.276
#&gt; SRR1975461     3  0.0000      0.894 0.000 0.000 1.000
#&gt; SRR1975462     3  0.0000      0.894 0.000 0.000 1.000
#&gt; SRR1975459     2  0.5859      0.875 0.000 0.656 0.344
#&gt; SRR1975460     2  0.5859      0.875 0.000 0.656 0.344
#&gt; SRR1975457     3  0.0000      0.894 0.000 0.000 1.000
#&gt; SRR1975458     3  0.0000      0.894 0.000 0.000 1.000
#&gt; SRR1975455     3  0.0000      0.894 0.000 0.000 1.000
#&gt; SRR1975456     3  0.0000      0.894 0.000 0.000 1.000
#&gt; SRR1975453     3  0.3686      0.781 0.000 0.140 0.860
#&gt; SRR1975454     3  0.3686      0.781 0.000 0.140 0.860
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-3'>
<p><a id='tab-ATC-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.1042      0.910 0.020 0.008 0.972 0.000
#&gt; SRR1975507     3  0.1042      0.910 0.020 0.008 0.972 0.000
#&gt; SRR1975506     3  0.1042      0.910 0.020 0.008 0.972 0.000
#&gt; SRR1975505     3  0.1042      0.910 0.020 0.008 0.972 0.000
#&gt; SRR1975503     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975504     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975501     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975502     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975499     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975500     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975497     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975498     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975493     2  0.0657      0.868 0.012 0.984 0.000 0.004
#&gt; SRR1975494     2  0.0657      0.868 0.012 0.984 0.000 0.004
#&gt; SRR1975495     1  0.3400      0.756 0.820 0.000 0.000 0.180
#&gt; SRR1975496     1  0.3400      0.756 0.820 0.000 0.000 0.180
#&gt; SRR1975491     4  0.0804      0.972 0.012 0.008 0.000 0.980
#&gt; SRR1975492     4  0.0804      0.972 0.012 0.008 0.000 0.980
#&gt; SRR1975489     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975487     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975488     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975485     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975486     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975483     1  0.4134      0.763 0.740 0.000 0.000 0.260
#&gt; SRR1975484     1  0.4134      0.763 0.740 0.000 0.000 0.260
#&gt; SRR1975481     1  0.4994      0.453 0.520 0.000 0.000 0.480
#&gt; SRR1975482     1  0.4994      0.453 0.520 0.000 0.000 0.480
#&gt; SRR1975477     3  0.0804      0.909 0.008 0.012 0.980 0.000
#&gt; SRR1975478     3  0.0804      0.909 0.008 0.012 0.980 0.000
#&gt; SRR1975479     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975480     4  0.0000      0.986 0.000 0.000 0.000 1.000
#&gt; SRR1975475     4  0.0336      0.981 0.008 0.000 0.000 0.992
#&gt; SRR1975476     4  0.0336      0.981 0.008 0.000 0.000 0.992
#&gt; SRR1975473     3  0.4994      0.705 0.048 0.208 0.744 0.000
#&gt; SRR1975474     3  0.4994      0.705 0.048 0.208 0.744 0.000
#&gt; SRR1975471     1  0.0895      0.579 0.976 0.004 0.020 0.000
#&gt; SRR1975472     1  0.0895      0.579 0.976 0.004 0.020 0.000
#&gt; SRR1975469     4  0.1792      0.905 0.068 0.000 0.000 0.932
#&gt; SRR1975470     4  0.1792      0.905 0.068 0.000 0.000 0.932
#&gt; SRR1975467     4  0.1174      0.962 0.012 0.020 0.000 0.968
#&gt; SRR1975468     4  0.1174      0.962 0.012 0.020 0.000 0.968
#&gt; SRR1975465     2  0.3266      0.882 0.000 0.832 0.168 0.000
#&gt; SRR1975466     2  0.3266      0.882 0.000 0.832 0.168 0.000
#&gt; SRR1975463     2  0.0895      0.882 0.004 0.976 0.020 0.000
#&gt; SRR1975464     2  0.0895      0.882 0.004 0.976 0.020 0.000
#&gt; SRR1975461     3  0.1798      0.900 0.040 0.016 0.944 0.000
#&gt; SRR1975462     3  0.1798      0.900 0.040 0.016 0.944 0.000
#&gt; SRR1975459     2  0.3444      0.870 0.000 0.816 0.184 0.000
#&gt; SRR1975460     2  0.3444      0.870 0.000 0.816 0.184 0.000
#&gt; SRR1975457     3  0.0524      0.910 0.004 0.008 0.988 0.000
#&gt; SRR1975458     3  0.0524      0.910 0.004 0.008 0.988 0.000
#&gt; SRR1975455     3  0.0524      0.910 0.004 0.008 0.988 0.000
#&gt; SRR1975456     3  0.0524      0.910 0.004 0.008 0.988 0.000
#&gt; SRR1975453     3  0.4690      0.723 0.260 0.016 0.724 0.000
#&gt; SRR1975454     3  0.4690      0.723 0.260 0.016 0.724 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-4'>
<p><a id='tab-ATC-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.4040      0.465 0.000 0.016 0.724 0.000 0.260
#&gt; SRR1975507     3  0.4040      0.465 0.000 0.016 0.724 0.000 0.260
#&gt; SRR1975506     3  0.4040      0.465 0.000 0.016 0.724 0.000 0.260
#&gt; SRR1975505     3  0.4040      0.465 0.000 0.016 0.724 0.000 0.260
#&gt; SRR1975503     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975504     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975501     4  0.1661      0.904 0.036 0.000 0.000 0.940 0.024
#&gt; SRR1975502     4  0.1661      0.904 0.036 0.000 0.000 0.940 0.024
#&gt; SRR1975499     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975500     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975497     4  0.0324      0.931 0.004 0.000 0.000 0.992 0.004
#&gt; SRR1975498     4  0.0324      0.931 0.004 0.000 0.000 0.992 0.004
#&gt; SRR1975493     2  0.2873      0.799 0.016 0.856 0.000 0.000 0.128
#&gt; SRR1975494     2  0.2873      0.799 0.016 0.856 0.000 0.000 0.128
#&gt; SRR1975495     1  0.2522      0.662 0.896 0.000 0.000 0.052 0.052
#&gt; SRR1975496     1  0.2522      0.662 0.896 0.000 0.000 0.052 0.052
#&gt; SRR1975491     4  0.2396      0.885 0.024 0.004 0.000 0.904 0.068
#&gt; SRR1975492     4  0.2396      0.885 0.024 0.004 0.000 0.904 0.068
#&gt; SRR1975489     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975490     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975487     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975488     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975485     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975486     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975483     1  0.2648      0.699 0.848 0.000 0.000 0.152 0.000
#&gt; SRR1975484     1  0.2648      0.699 0.848 0.000 0.000 0.152 0.000
#&gt; SRR1975481     1  0.4583      0.600 0.672 0.000 0.000 0.296 0.032
#&gt; SRR1975482     1  0.4583      0.600 0.672 0.000 0.000 0.296 0.032
#&gt; SRR1975477     3  0.2583      0.604 0.000 0.004 0.864 0.000 0.132
#&gt; SRR1975478     3  0.2583      0.604 0.000 0.004 0.864 0.000 0.132
#&gt; SRR1975479     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975480     4  0.0000      0.934 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975475     4  0.0671      0.925 0.004 0.000 0.000 0.980 0.016
#&gt; SRR1975476     4  0.0671      0.925 0.004 0.000 0.000 0.980 0.016
#&gt; SRR1975473     3  0.5760      0.366 0.028 0.092 0.660 0.000 0.220
#&gt; SRR1975474     3  0.5760      0.366 0.028 0.092 0.660 0.000 0.220
#&gt; SRR1975471     1  0.4242      0.274 0.572 0.000 0.000 0.000 0.428
#&gt; SRR1975472     1  0.4242      0.274 0.572 0.000 0.000 0.000 0.428
#&gt; SRR1975469     4  0.4525      0.340 0.360 0.000 0.000 0.624 0.016
#&gt; SRR1975470     4  0.4525      0.340 0.360 0.000 0.000 0.624 0.016
#&gt; SRR1975467     4  0.2753      0.849 0.008 0.012 0.000 0.876 0.104
#&gt; SRR1975468     4  0.2753      0.849 0.008 0.012 0.000 0.876 0.104
#&gt; SRR1975465     2  0.3181      0.858 0.000 0.856 0.072 0.000 0.072
#&gt; SRR1975466     2  0.3181      0.858 0.000 0.856 0.072 0.000 0.072
#&gt; SRR1975463     2  0.0404      0.858 0.000 0.988 0.012 0.000 0.000
#&gt; SRR1975464     2  0.0404      0.858 0.000 0.988 0.012 0.000 0.000
#&gt; SRR1975461     3  0.4781     -0.131 0.000 0.020 0.552 0.000 0.428
#&gt; SRR1975462     3  0.4781     -0.131 0.000 0.020 0.552 0.000 0.428
#&gt; SRR1975459     2  0.3812      0.830 0.000 0.812 0.092 0.000 0.096
#&gt; SRR1975460     2  0.3812      0.830 0.000 0.812 0.092 0.000 0.096
#&gt; SRR1975457     3  0.0000      0.632 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975458     3  0.0000      0.632 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975455     3  0.0000      0.632 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975456     3  0.0000      0.632 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975453     5  0.5568      1.000 0.060 0.016 0.308 0.000 0.616
#&gt; SRR1975454     5  0.5568      1.000 0.060 0.016 0.308 0.000 0.616
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-5'>
<p><a id='tab-ATC-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     3  0.0146     0.5924 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR1975507     3  0.0146     0.5924 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR1975506     3  0.0146     0.5924 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR1975505     3  0.0146     0.5924 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR1975503     4  0.0146     0.8777 0.000 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1975504     4  0.0146     0.8777 0.000 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1975501     4  0.2537     0.8107 0.088 0.000 0.000 0.880 0.024 0.008
#&gt; SRR1975502     4  0.2537     0.8107 0.088 0.000 0.000 0.880 0.024 0.008
#&gt; SRR1975499     4  0.0000     0.8788 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975500     4  0.0000     0.8788 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975497     4  0.0922     0.8663 0.024 0.000 0.000 0.968 0.004 0.004
#&gt; SRR1975498     4  0.0922     0.8663 0.024 0.000 0.000 0.968 0.004 0.004
#&gt; SRR1975493     2  0.5621     0.5945 0.060 0.648 0.000 0.000 0.172 0.120
#&gt; SRR1975494     2  0.5621     0.5945 0.060 0.648 0.000 0.000 0.172 0.120
#&gt; SRR1975495     1  0.4224     0.5890 0.684 0.000 0.000 0.036 0.004 0.276
#&gt; SRR1975496     1  0.4224     0.5890 0.684 0.000 0.000 0.036 0.004 0.276
#&gt; SRR1975491     4  0.4177     0.7363 0.116 0.000 0.000 0.780 0.064 0.040
#&gt; SRR1975492     4  0.4177     0.7363 0.116 0.000 0.000 0.780 0.064 0.040
#&gt; SRR1975489     4  0.0000     0.8788 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975490     4  0.0000     0.8788 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975487     4  0.0000     0.8788 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975488     4  0.0000     0.8788 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975485     4  0.0000     0.8788 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975486     4  0.0000     0.8788 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975483     1  0.3644     0.7384 0.792 0.000 0.000 0.120 0.000 0.088
#&gt; SRR1975484     1  0.3644     0.7384 0.792 0.000 0.000 0.120 0.000 0.088
#&gt; SRR1975481     1  0.3930     0.6560 0.728 0.000 0.000 0.236 0.032 0.004
#&gt; SRR1975482     1  0.3930     0.6560 0.728 0.000 0.000 0.236 0.032 0.004
#&gt; SRR1975477     3  0.4264    -0.1289 0.000 0.016 0.496 0.000 0.488 0.000
#&gt; SRR1975478     3  0.4264    -0.1289 0.000 0.016 0.496 0.000 0.488 0.000
#&gt; SRR1975479     4  0.0000     0.8788 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975480     4  0.0000     0.8788 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975475     4  0.0891     0.8670 0.008 0.000 0.000 0.968 0.024 0.000
#&gt; SRR1975476     4  0.0891     0.8670 0.008 0.000 0.000 0.968 0.024 0.000
#&gt; SRR1975473     5  0.3437     1.0000 0.008 0.012 0.188 0.000 0.788 0.004
#&gt; SRR1975474     5  0.3437     1.0000 0.008 0.012 0.188 0.000 0.788 0.004
#&gt; SRR1975471     6  0.3089     0.5163 0.188 0.000 0.008 0.000 0.004 0.800
#&gt; SRR1975472     6  0.3089     0.5163 0.188 0.000 0.008 0.000 0.004 0.800
#&gt; SRR1975469     4  0.4797    -0.0362 0.460 0.000 0.000 0.500 0.024 0.016
#&gt; SRR1975470     4  0.4797    -0.0362 0.460 0.000 0.000 0.500 0.024 0.016
#&gt; SRR1975467     4  0.6119     0.5419 0.092 0.024 0.000 0.644 0.144 0.096
#&gt; SRR1975468     4  0.6119     0.5419 0.092 0.024 0.000 0.644 0.144 0.096
#&gt; SRR1975465     2  0.2632     0.8069 0.000 0.832 0.164 0.000 0.000 0.004
#&gt; SRR1975466     2  0.2632     0.8069 0.000 0.832 0.164 0.000 0.000 0.004
#&gt; SRR1975463     2  0.1149     0.7880 0.000 0.960 0.024 0.000 0.008 0.008
#&gt; SRR1975464     2  0.1149     0.7880 0.000 0.960 0.024 0.000 0.008 0.008
#&gt; SRR1975461     3  0.2636     0.4501 0.000 0.004 0.860 0.000 0.016 0.120
#&gt; SRR1975462     3  0.2636     0.4501 0.000 0.004 0.860 0.000 0.016 0.120
#&gt; SRR1975459     2  0.2738     0.8015 0.000 0.820 0.176 0.000 0.000 0.004
#&gt; SRR1975460     2  0.2738     0.8015 0.000 0.820 0.176 0.000 0.000 0.004
#&gt; SRR1975457     3  0.4502     0.2521 0.012 0.000 0.568 0.000 0.404 0.016
#&gt; SRR1975458     3  0.4502     0.2521 0.012 0.000 0.568 0.000 0.404 0.016
#&gt; SRR1975455     3  0.4494     0.2604 0.012 0.000 0.572 0.000 0.400 0.016
#&gt; SRR1975456     3  0.4494     0.2604 0.012 0.000 0.572 0.000 0.400 0.016
#&gt; SRR1975453     6  0.4301     0.5300 0.000 0.004 0.400 0.000 0.016 0.580
#&gt; SRR1975454     6  0.4301     0.5300 0.000 0.004 0.400 0.000 0.016 0.580
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-skmeans-signature_compare](figure_cola/ATC-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-skmeans-collect-classes](figure_cola/ATC-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "pam"]
# you can also extract it by
# res = res_list["ATC:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-pam-collect-plots](figure_cola/ATC-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-pam-select-partition-number](figure_cola/ATC-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.981       0.969         0.4819 0.494   0.494
#> 3 3 1.000           0.960       0.982         0.1958 0.922   0.842
#> 4 4 0.678           0.672       0.856         0.2110 0.808   0.577
#> 5 5 0.755           0.673       0.831         0.0664 0.844   0.549
#> 6 6 0.884           0.823       0.928         0.0537 0.953   0.811
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-classes'>
<ul>
<li><a href='#tab-ATC-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-pam-get-classes-1'>
<p><a id='tab-ATC-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2   0.000      0.929 0.000 1.000
#&gt; SRR1975507     2   0.000      0.929 0.000 1.000
#&gt; SRR1975506     2   0.000      0.929 0.000 1.000
#&gt; SRR1975505     2   0.000      0.929 0.000 1.000
#&gt; SRR1975503     1   0.000      1.000 1.000 0.000
#&gt; SRR1975504     1   0.000      1.000 1.000 0.000
#&gt; SRR1975501     1   0.000      1.000 1.000 0.000
#&gt; SRR1975502     1   0.000      1.000 1.000 0.000
#&gt; SRR1975499     1   0.000      1.000 1.000 0.000
#&gt; SRR1975500     1   0.000      1.000 1.000 0.000
#&gt; SRR1975497     1   0.000      1.000 1.000 0.000
#&gt; SRR1975498     1   0.000      1.000 1.000 0.000
#&gt; SRR1975493     2   0.605      0.908 0.148 0.852
#&gt; SRR1975494     2   0.563      0.926 0.132 0.868
#&gt; SRR1975495     1   0.000      1.000 1.000 0.000
#&gt; SRR1975496     1   0.000      1.000 1.000 0.000
#&gt; SRR1975491     1   0.000      1.000 1.000 0.000
#&gt; SRR1975492     1   0.000      1.000 1.000 0.000
#&gt; SRR1975489     1   0.000      1.000 1.000 0.000
#&gt; SRR1975490     1   0.000      1.000 1.000 0.000
#&gt; SRR1975487     1   0.000      1.000 1.000 0.000
#&gt; SRR1975488     1   0.000      1.000 1.000 0.000
#&gt; SRR1975485     1   0.000      1.000 1.000 0.000
#&gt; SRR1975486     1   0.000      1.000 1.000 0.000
#&gt; SRR1975483     1   0.000      1.000 1.000 0.000
#&gt; SRR1975484     1   0.000      1.000 1.000 0.000
#&gt; SRR1975481     1   0.000      1.000 1.000 0.000
#&gt; SRR1975482     1   0.000      1.000 1.000 0.000
#&gt; SRR1975477     2   0.402      0.974 0.080 0.920
#&gt; SRR1975478     2   0.402      0.974 0.080 0.920
#&gt; SRR1975479     1   0.000      1.000 1.000 0.000
#&gt; SRR1975480     1   0.000      1.000 1.000 0.000
#&gt; SRR1975475     1   0.000      1.000 1.000 0.000
#&gt; SRR1975476     1   0.000      1.000 1.000 0.000
#&gt; SRR1975473     2   0.402      0.974 0.080 0.920
#&gt; SRR1975474     2   0.402      0.974 0.080 0.920
#&gt; SRR1975471     2   0.402      0.974 0.080 0.920
#&gt; SRR1975472     2   0.402      0.974 0.080 0.920
#&gt; SRR1975469     1   0.000      1.000 1.000 0.000
#&gt; SRR1975470     1   0.000      1.000 1.000 0.000
#&gt; SRR1975467     1   0.000      1.000 1.000 0.000
#&gt; SRR1975468     1   0.000      1.000 1.000 0.000
#&gt; SRR1975465     2   0.402      0.974 0.080 0.920
#&gt; SRR1975466     2   0.402      0.974 0.080 0.920
#&gt; SRR1975463     2   0.402      0.974 0.080 0.920
#&gt; SRR1975464     2   0.402      0.974 0.080 0.920
#&gt; SRR1975461     2   0.000      0.929 0.000 1.000
#&gt; SRR1975462     2   0.000      0.929 0.000 1.000
#&gt; SRR1975459     2   0.402      0.974 0.080 0.920
#&gt; SRR1975460     2   0.402      0.974 0.080 0.920
#&gt; SRR1975457     2   0.402      0.974 0.080 0.920
#&gt; SRR1975458     2   0.402      0.974 0.080 0.920
#&gt; SRR1975455     2   0.402      0.974 0.080 0.920
#&gt; SRR1975456     2   0.402      0.974 0.080 0.920
#&gt; SRR1975453     2   0.402      0.974 0.080 0.920
#&gt; SRR1975454     2   0.402      0.974 0.080 0.920
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-1-a').click(function(){
  $('#tab-ATC-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-2'>
<p><a id='tab-ATC-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3   0.000      0.818 0.000 0.000 1.000
#&gt; SRR1975507     3   0.000      0.818 0.000 0.000 1.000
#&gt; SRR1975506     3   0.000      0.818 0.000 0.000 1.000
#&gt; SRR1975505     3   0.000      0.818 0.000 0.000 1.000
#&gt; SRR1975503     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975504     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975501     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975502     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975499     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975500     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975497     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975498     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975493     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975494     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975495     1   0.175      0.941 0.952 0.048 0.000
#&gt; SRR1975496     1   0.207      0.926 0.940 0.060 0.000
#&gt; SRR1975491     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975492     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975489     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975490     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975487     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975488     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975485     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975486     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975483     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975484     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975481     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975482     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975477     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975478     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975479     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975480     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975475     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975476     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975473     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975474     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975471     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975472     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975469     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975470     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975467     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975468     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1975465     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975466     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975463     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975464     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975461     3   0.626      0.345 0.000 0.448 0.552
#&gt; SRR1975462     3   0.621      0.393 0.000 0.428 0.572
#&gt; SRR1975459     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975460     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975457     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975458     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975455     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975456     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975453     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR1975454     2   0.000      1.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-2-a').click(function(){
  $('#tab-ATC-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-3'>
<p><a id='tab-ATC-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1975503     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975504     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975501     4  0.1059      0.857 0.016 0.012 0.000 0.972
#&gt; SRR1975502     4  0.1182      0.855 0.016 0.016 0.000 0.968
#&gt; SRR1975499     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975500     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975497     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975498     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975493     2  0.0000      0.368 0.000 1.000 0.000 0.000
#&gt; SRR1975494     2  0.0000      0.368 0.000 1.000 0.000 0.000
#&gt; SRR1975495     1  0.7314      0.596 0.488 0.348 0.000 0.164
#&gt; SRR1975496     1  0.7314      0.596 0.488 0.348 0.000 0.164
#&gt; SRR1975491     4  0.6039      0.482 0.056 0.348 0.000 0.596
#&gt; SRR1975492     4  0.6039      0.482 0.056 0.348 0.000 0.596
#&gt; SRR1975489     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975487     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975488     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975485     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975486     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975483     1  0.7314      0.596 0.488 0.348 0.000 0.164
#&gt; SRR1975484     1  0.7314      0.596 0.488 0.348 0.000 0.164
#&gt; SRR1975481     1  0.7404      0.587 0.476 0.348 0.000 0.176
#&gt; SRR1975482     1  0.7404      0.587 0.476 0.348 0.000 0.176
#&gt; SRR1975477     2  0.4661      0.851 0.348 0.652 0.000 0.000
#&gt; SRR1975478     2  0.4661      0.851 0.348 0.652 0.000 0.000
#&gt; SRR1975479     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975480     4  0.0000      0.870 0.000 0.000 0.000 1.000
#&gt; SRR1975475     4  0.0524      0.866 0.008 0.004 0.000 0.988
#&gt; SRR1975476     4  0.0524      0.866 0.008 0.004 0.000 0.988
#&gt; SRR1975473     2  0.4790      0.620 0.380 0.620 0.000 0.000
#&gt; SRR1975474     2  0.4790      0.620 0.380 0.620 0.000 0.000
#&gt; SRR1975471     1  0.4697      0.543 0.644 0.356 0.000 0.000
#&gt; SRR1975472     1  0.4697      0.543 0.644 0.356 0.000 0.000
#&gt; SRR1975469     4  0.6039      0.482 0.056 0.348 0.000 0.596
#&gt; SRR1975470     4  0.6039      0.482 0.056 0.348 0.000 0.596
#&gt; SRR1975467     4  0.6039      0.482 0.056 0.348 0.000 0.596
#&gt; SRR1975468     4  0.6039      0.482 0.056 0.348 0.000 0.596
#&gt; SRR1975465     2  0.4697      0.853 0.356 0.644 0.000 0.000
#&gt; SRR1975466     2  0.4697      0.853 0.356 0.644 0.000 0.000
#&gt; SRR1975463     2  0.4697      0.853 0.356 0.644 0.000 0.000
#&gt; SRR1975464     2  0.4697      0.853 0.356 0.644 0.000 0.000
#&gt; SRR1975461     1  0.6065      0.176 0.684 0.140 0.176 0.000
#&gt; SRR1975462     1  0.6104      0.180 0.680 0.140 0.180 0.000
#&gt; SRR1975459     2  0.4697      0.853 0.356 0.644 0.000 0.000
#&gt; SRR1975460     2  0.4697      0.853 0.356 0.644 0.000 0.000
#&gt; SRR1975457     1  0.4431     -0.350 0.696 0.304 0.000 0.000
#&gt; SRR1975458     1  0.4543     -0.396 0.676 0.324 0.000 0.000
#&gt; SRR1975455     2  0.4817      0.829 0.388 0.612 0.000 0.000
#&gt; SRR1975456     2  0.4843      0.822 0.396 0.604 0.000 0.000
#&gt; SRR1975453     1  0.1557      0.206 0.944 0.056 0.000 0.000
#&gt; SRR1975454     1  0.1557      0.206 0.944 0.056 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-3-a').click(function(){
  $('#tab-ATC-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-4'>
<p><a id='tab-ATC-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975503     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975504     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975501     4  0.1965      0.824 0.096 0.000 0.000 0.904 0.000
#&gt; SRR1975502     4  0.2020      0.819 0.100 0.000 0.000 0.900 0.000
#&gt; SRR1975499     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975500     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975497     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975498     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975493     2  0.5874      0.427 0.364 0.528 0.000 0.000 0.108
#&gt; SRR1975494     2  0.5874      0.427 0.364 0.528 0.000 0.000 0.108
#&gt; SRR1975495     1  0.1792      0.661 0.916 0.000 0.000 0.084 0.000
#&gt; SRR1975496     1  0.1792      0.661 0.916 0.000 0.000 0.084 0.000
#&gt; SRR1975491     1  0.4307      0.139 0.504 0.000 0.000 0.496 0.000
#&gt; SRR1975492     1  0.4306      0.151 0.508 0.000 0.000 0.492 0.000
#&gt; SRR1975489     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975490     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975487     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975488     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975485     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975486     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975483     1  0.1792      0.661 0.916 0.000 0.000 0.084 0.000
#&gt; SRR1975484     1  0.1792      0.661 0.916 0.000 0.000 0.084 0.000
#&gt; SRR1975481     1  0.1965      0.661 0.904 0.000 0.000 0.096 0.000
#&gt; SRR1975482     1  0.1965      0.661 0.904 0.000 0.000 0.096 0.000
#&gt; SRR1975477     5  0.0000      0.875 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975478     5  0.0000      0.875 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975479     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975480     4  0.0000      0.918 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975475     4  0.0404      0.909 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1975476     4  0.0404      0.909 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1975473     5  0.5404      0.525 0.152 0.184 0.000 0.000 0.664
#&gt; SRR1975474     5  0.5404      0.525 0.152 0.184 0.000 0.000 0.664
#&gt; SRR1975471     1  0.2074      0.528 0.896 0.104 0.000 0.000 0.000
#&gt; SRR1975472     1  0.2074      0.528 0.896 0.104 0.000 0.000 0.000
#&gt; SRR1975469     1  0.4304      0.173 0.516 0.000 0.000 0.484 0.000
#&gt; SRR1975470     1  0.4302      0.182 0.520 0.000 0.000 0.480 0.000
#&gt; SRR1975467     4  0.4300     -0.154 0.476 0.000 0.000 0.524 0.000
#&gt; SRR1975468     4  0.4300     -0.154 0.476 0.000 0.000 0.524 0.000
#&gt; SRR1975465     2  0.3534      0.720 0.000 0.744 0.000 0.000 0.256
#&gt; SRR1975466     2  0.3534      0.720 0.000 0.744 0.000 0.000 0.256
#&gt; SRR1975463     2  0.3534      0.720 0.000 0.744 0.000 0.000 0.256
#&gt; SRR1975464     2  0.3534      0.720 0.000 0.744 0.000 0.000 0.256
#&gt; SRR1975461     2  0.4185      0.468 0.084 0.816 0.052 0.000 0.048
#&gt; SRR1975462     2  0.4185      0.468 0.084 0.816 0.052 0.000 0.048
#&gt; SRR1975459     2  0.3534      0.720 0.000 0.744 0.000 0.000 0.256
#&gt; SRR1975460     2  0.3534      0.720 0.000 0.744 0.000 0.000 0.256
#&gt; SRR1975457     5  0.0290      0.871 0.000 0.008 0.000 0.000 0.992
#&gt; SRR1975458     5  0.0290      0.871 0.000 0.008 0.000 0.000 0.992
#&gt; SRR1975455     5  0.0000      0.875 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975456     5  0.0000      0.875 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1975453     1  0.6077     -0.203 0.480 0.124 0.000 0.000 0.396
#&gt; SRR1975454     1  0.6077     -0.203 0.480 0.124 0.000 0.000 0.396
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-4-a').click(function(){
  $('#tab-ATC-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-5'>
<p><a id='tab-ATC-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5    p6
#&gt; SRR1975508     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975507     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975506     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975505     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1975503     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975504     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975501     4  0.2664      0.732 0.184 0.000  0 0.816 0.000 0.000
#&gt; SRR1975502     4  0.2697      0.726 0.188 0.000  0 0.812 0.000 0.000
#&gt; SRR1975499     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975500     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975497     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975498     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975493     2  0.0632      0.967 0.024 0.976  0 0.000 0.000 0.000
#&gt; SRR1975494     2  0.0632      0.967 0.024 0.976  0 0.000 0.000 0.000
#&gt; SRR1975495     1  0.0000      0.774 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.774 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1975491     1  0.3706      0.387 0.620 0.000  0 0.380 0.000 0.000
#&gt; SRR1975492     1  0.3647      0.433 0.640 0.000  0 0.360 0.000 0.000
#&gt; SRR1975489     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975490     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975487     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975488     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975485     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975486     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975483     1  0.0000      0.774 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.774 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0146      0.774 0.996 0.000  0 0.004 0.000 0.000
#&gt; SRR1975482     1  0.0146      0.774 0.996 0.000  0 0.004 0.000 0.000
#&gt; SRR1975477     5  0.0547      0.974 0.000 0.020  0 0.000 0.980 0.000
#&gt; SRR1975478     5  0.0547      0.974 0.000 0.020  0 0.000 0.980 0.000
#&gt; SRR1975479     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975480     4  0.0000      0.911 0.000 0.000  0 1.000 0.000 0.000
#&gt; SRR1975475     4  0.0865      0.887 0.036 0.000  0 0.964 0.000 0.000
#&gt; SRR1975476     4  0.0865      0.887 0.036 0.000  0 0.964 0.000 0.000
#&gt; SRR1975473     2  0.1152      0.953 0.004 0.952  0 0.000 0.044 0.000
#&gt; SRR1975474     2  0.1152      0.953 0.004 0.952  0 0.000 0.044 0.000
#&gt; SRR1975471     1  0.3446      0.431 0.692 0.000  0 0.000 0.000 0.308
#&gt; SRR1975472     1  0.3446      0.431 0.692 0.000  0 0.000 0.000 0.308
#&gt; SRR1975469     1  0.2762      0.684 0.804 0.000  0 0.196 0.000 0.000
#&gt; SRR1975470     1  0.2491      0.707 0.836 0.000  0 0.164 0.000 0.000
#&gt; SRR1975467     4  0.3867     -0.054 0.488 0.000  0 0.512 0.000 0.000
#&gt; SRR1975468     4  0.3867     -0.054 0.488 0.000  0 0.512 0.000 0.000
#&gt; SRR1975465     2  0.0000      0.981 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000      0.981 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0000      0.981 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975464     2  0.0000      0.981 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975461     6  0.0000      0.740 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1975462     6  0.0000      0.740 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1975459     2  0.0000      0.981 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975460     2  0.0000      0.981 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1975457     5  0.0000      0.987 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975458     5  0.0000      0.987 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975455     5  0.0000      0.987 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975456     5  0.0000      0.987 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1975453     6  0.4471      0.686 0.020 0.020  0 0.000 0.312 0.648
#&gt; SRR1975454     6  0.4471      0.686 0.020 0.020  0 0.000 0.312 0.648
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-5-a').click(function(){
  $('#tab-ATC-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-pam-signature_compare](figure_cola/ATC-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-pam-collect-classes](figure_cola/ATC-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "mclust"]
# you can also extract it by
# res = res_list["ATC:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-mclust-collect-plots](figure_cola/ATC-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-mclust-select-partition-number](figure_cola/ATC-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.982       0.988         0.4214 0.584   0.584
#> 3 3 0.441           0.852       0.866         0.2238 0.530   0.403
#> 4 4 0.631           0.773       0.887         0.3562 0.725   0.488
#> 5 5 0.796           0.773       0.862         0.0851 0.964   0.870
#> 6 6 0.841           0.821       0.922         0.0646 0.948   0.787
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-classes'>
<ul>
<li><a href='#tab-ATC-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-mclust-get-classes-1'>
<p><a id='tab-ATC-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975507     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975506     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975505     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975503     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975504     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975501     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975502     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975499     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975500     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975497     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975498     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975493     1  0.3431      0.947 0.936 0.064
#&gt; SRR1975494     1  0.3431      0.947 0.936 0.064
#&gt; SRR1975495     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975496     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975491     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975492     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975489     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975490     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975487     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975488     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975485     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975486     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975483     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975484     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975481     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975482     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975477     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975478     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975479     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975480     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975475     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975476     1  0.0000      0.984 1.000 0.000
#&gt; SRR1975473     2  0.1184      0.984 0.016 0.984
#&gt; SRR1975474     2  0.1184      0.984 0.016 0.984
#&gt; SRR1975471     1  0.0938      0.981 0.988 0.012
#&gt; SRR1975472     1  0.0938      0.981 0.988 0.012
#&gt; SRR1975469     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975470     1  0.0376      0.984 0.996 0.004
#&gt; SRR1975467     1  0.1633      0.973 0.976 0.024
#&gt; SRR1975468     1  0.1633      0.973 0.976 0.024
#&gt; SRR1975465     1  0.3431      0.947 0.936 0.064
#&gt; SRR1975466     1  0.3431      0.947 0.936 0.064
#&gt; SRR1975463     1  0.3431      0.947 0.936 0.064
#&gt; SRR1975464     1  0.3431      0.947 0.936 0.064
#&gt; SRR1975461     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975462     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975459     1  0.3431      0.947 0.936 0.064
#&gt; SRR1975460     1  0.3431      0.947 0.936 0.064
#&gt; SRR1975457     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975458     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975455     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975456     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975453     2  0.0000      0.998 0.000 1.000
#&gt; SRR1975454     2  0.0000      0.998 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-1-a').click(function(){
  $('#tab-ATC-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-2'>
<p><a id='tab-ATC-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3   0.153      1.000 0.000 0.040 0.960
#&gt; SRR1975507     3   0.153      1.000 0.000 0.040 0.960
#&gt; SRR1975506     3   0.153      1.000 0.000 0.040 0.960
#&gt; SRR1975505     3   0.153      1.000 0.000 0.040 0.960
#&gt; SRR1975503     1   0.288      0.857 0.904 0.096 0.000
#&gt; SRR1975504     1   0.288      0.857 0.904 0.096 0.000
#&gt; SRR1975501     2   0.546      0.821 0.184 0.788 0.028
#&gt; SRR1975502     2   0.546      0.821 0.184 0.788 0.028
#&gt; SRR1975499     1   0.000      0.970 1.000 0.000 0.000
#&gt; SRR1975500     1   0.000      0.970 1.000 0.000 0.000
#&gt; SRR1975497     2   0.568      0.741 0.316 0.684 0.000
#&gt; SRR1975498     2   0.568      0.741 0.316 0.684 0.000
#&gt; SRR1975493     2   0.359      0.808 0.088 0.892 0.020
#&gt; SRR1975494     2   0.359      0.808 0.088 0.892 0.020
#&gt; SRR1975495     2   0.533      0.821 0.184 0.792 0.024
#&gt; SRR1975496     2   0.533      0.821 0.184 0.792 0.024
#&gt; SRR1975491     2   0.573      0.748 0.324 0.676 0.000
#&gt; SRR1975492     2   0.573      0.748 0.324 0.676 0.000
#&gt; SRR1975489     1   0.000      0.970 1.000 0.000 0.000
#&gt; SRR1975490     1   0.000      0.970 1.000 0.000 0.000
#&gt; SRR1975487     1   0.000      0.970 1.000 0.000 0.000
#&gt; SRR1975488     1   0.000      0.970 1.000 0.000 0.000
#&gt; SRR1975485     1   0.000      0.970 1.000 0.000 0.000
#&gt; SRR1975486     1   0.000      0.970 1.000 0.000 0.000
#&gt; SRR1975483     2   0.533      0.821 0.184 0.792 0.024
#&gt; SRR1975484     2   0.533      0.821 0.184 0.792 0.024
#&gt; SRR1975481     2   0.533      0.821 0.184 0.792 0.024
#&gt; SRR1975482     2   0.533      0.821 0.184 0.792 0.024
#&gt; SRR1975477     2   0.298      0.809 0.024 0.920 0.056
#&gt; SRR1975478     2   0.298      0.809 0.024 0.920 0.056
#&gt; SRR1975479     1   0.000      0.970 1.000 0.000 0.000
#&gt; SRR1975480     1   0.000      0.970 1.000 0.000 0.000
#&gt; SRR1975475     1   0.103      0.950 0.976 0.024 0.000
#&gt; SRR1975476     1   0.103      0.950 0.976 0.024 0.000
#&gt; SRR1975473     2   0.298      0.809 0.024 0.920 0.056
#&gt; SRR1975474     2   0.298      0.809 0.024 0.920 0.056
#&gt; SRR1975471     2   0.535      0.823 0.176 0.796 0.028
#&gt; SRR1975472     2   0.535      0.823 0.176 0.796 0.028
#&gt; SRR1975469     2   0.533      0.821 0.184 0.792 0.024
#&gt; SRR1975470     2   0.533      0.821 0.184 0.792 0.024
#&gt; SRR1975467     2   0.603      0.789 0.272 0.712 0.016
#&gt; SRR1975468     2   0.606      0.787 0.276 0.708 0.016
#&gt; SRR1975465     2   0.336      0.811 0.084 0.900 0.016
#&gt; SRR1975466     2   0.336      0.811 0.084 0.900 0.016
#&gt; SRR1975463     2   0.336      0.811 0.084 0.900 0.016
#&gt; SRR1975464     2   0.336      0.811 0.084 0.900 0.016
#&gt; SRR1975461     2   0.424      0.761 0.000 0.824 0.176
#&gt; SRR1975462     2   0.424      0.761 0.000 0.824 0.176
#&gt; SRR1975459     2   0.336      0.811 0.084 0.900 0.016
#&gt; SRR1975460     2   0.336      0.811 0.084 0.900 0.016
#&gt; SRR1975457     2   0.305      0.807 0.020 0.916 0.064
#&gt; SRR1975458     2   0.305      0.807 0.020 0.916 0.064
#&gt; SRR1975455     2   0.305      0.807 0.020 0.916 0.064
#&gt; SRR1975456     2   0.305      0.807 0.020 0.916 0.064
#&gt; SRR1975453     2   0.418      0.762 0.000 0.828 0.172
#&gt; SRR1975454     2   0.418      0.762 0.000 0.828 0.172
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-2-a').click(function(){
  $('#tab-ATC-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-3'>
<p><a id='tab-ATC-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.0000     1.0000 0.000 0.000 1.000 0.000
#&gt; SRR1975507     3  0.0000     1.0000 0.000 0.000 1.000 0.000
#&gt; SRR1975506     3  0.0000     1.0000 0.000 0.000 1.000 0.000
#&gt; SRR1975505     3  0.0000     1.0000 0.000 0.000 1.000 0.000
#&gt; SRR1975503     4  0.5116     0.7115 0.108 0.128 0.000 0.764
#&gt; SRR1975504     4  0.5116     0.7115 0.108 0.128 0.000 0.764
#&gt; SRR1975501     1  0.1022     0.9302 0.968 0.000 0.000 0.032
#&gt; SRR1975502     1  0.1022     0.9302 0.968 0.000 0.000 0.032
#&gt; SRR1975499     4  0.0707     0.8613 0.000 0.020 0.000 0.980
#&gt; SRR1975500     4  0.0707     0.8613 0.000 0.020 0.000 0.980
#&gt; SRR1975497     1  0.4356     0.6150 0.708 0.000 0.000 0.292
#&gt; SRR1975498     1  0.4356     0.6150 0.708 0.000 0.000 0.292
#&gt; SRR1975493     2  0.2011     0.7181 0.000 0.920 0.000 0.080
#&gt; SRR1975494     2  0.2011     0.7181 0.000 0.920 0.000 0.080
#&gt; SRR1975495     1  0.0921     0.9291 0.972 0.000 0.000 0.028
#&gt; SRR1975496     1  0.0921     0.9291 0.972 0.000 0.000 0.028
#&gt; SRR1975491     4  0.7315     0.3423 0.252 0.216 0.000 0.532
#&gt; SRR1975492     4  0.7310     0.3437 0.256 0.212 0.000 0.532
#&gt; SRR1975489     4  0.0000     0.8611 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4  0.0000     0.8611 0.000 0.000 0.000 1.000
#&gt; SRR1975487     4  0.0000     0.8611 0.000 0.000 0.000 1.000
#&gt; SRR1975488     4  0.0000     0.8611 0.000 0.000 0.000 1.000
#&gt; SRR1975485     4  0.0000     0.8611 0.000 0.000 0.000 1.000
#&gt; SRR1975486     4  0.0000     0.8611 0.000 0.000 0.000 1.000
#&gt; SRR1975483     1  0.1022     0.9302 0.968 0.000 0.000 0.032
#&gt; SRR1975484     1  0.1022     0.9302 0.968 0.000 0.000 0.032
#&gt; SRR1975481     1  0.1022     0.9302 0.968 0.000 0.000 0.032
#&gt; SRR1975482     1  0.1022     0.9302 0.968 0.000 0.000 0.032
#&gt; SRR1975477     2  0.3790     0.7421 0.164 0.820 0.000 0.016
#&gt; SRR1975478     2  0.3790     0.7421 0.164 0.820 0.000 0.016
#&gt; SRR1975479     4  0.1888     0.8484 0.016 0.044 0.000 0.940
#&gt; SRR1975480     4  0.1888     0.8484 0.016 0.044 0.000 0.940
#&gt; SRR1975475     4  0.3013     0.8350 0.032 0.080 0.000 0.888
#&gt; SRR1975476     4  0.3037     0.8352 0.036 0.076 0.000 0.888
#&gt; SRR1975473     2  0.3790     0.7421 0.164 0.820 0.000 0.016
#&gt; SRR1975474     2  0.3790     0.7421 0.164 0.820 0.000 0.016
#&gt; SRR1975471     1  0.0000     0.9146 1.000 0.000 0.000 0.000
#&gt; SRR1975472     1  0.0000     0.9146 1.000 0.000 0.000 0.000
#&gt; SRR1975469     1  0.1022     0.9302 0.968 0.000 0.000 0.032
#&gt; SRR1975470     1  0.1022     0.9302 0.968 0.000 0.000 0.032
#&gt; SRR1975467     2  0.5500    -0.0385 0.016 0.520 0.000 0.464
#&gt; SRR1975468     2  0.5500    -0.0385 0.016 0.520 0.000 0.464
#&gt; SRR1975465     2  0.0188     0.7355 0.000 0.996 0.000 0.004
#&gt; SRR1975466     2  0.0188     0.7355 0.000 0.996 0.000 0.004
#&gt; SRR1975463     2  0.1302     0.7324 0.000 0.956 0.000 0.044
#&gt; SRR1975464     2  0.1302     0.7324 0.000 0.956 0.000 0.044
#&gt; SRR1975461     1  0.2081     0.8774 0.916 0.000 0.084 0.000
#&gt; SRR1975462     1  0.2081     0.8774 0.916 0.000 0.084 0.000
#&gt; SRR1975459     2  0.0188     0.7341 0.000 0.996 0.004 0.000
#&gt; SRR1975460     2  0.0188     0.7341 0.000 0.996 0.004 0.000
#&gt; SRR1975457     2  0.5220     0.5411 0.352 0.632 0.000 0.016
#&gt; SRR1975458     2  0.5220     0.5411 0.352 0.632 0.000 0.016
#&gt; SRR1975455     2  0.4980     0.6188 0.304 0.680 0.000 0.016
#&gt; SRR1975456     2  0.4980     0.6188 0.304 0.680 0.000 0.016
#&gt; SRR1975453     1  0.2081     0.8774 0.916 0.000 0.084 0.000
#&gt; SRR1975454     1  0.2081     0.8774 0.916 0.000 0.084 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-3-a').click(function(){
  $('#tab-ATC-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-4'>
<p><a id='tab-ATC-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975507     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975506     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975505     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1975503     4  0.2959     0.8553 0.036 0.100 0.000 0.864 0.000
#&gt; SRR1975504     4  0.2959     0.8553 0.036 0.100 0.000 0.864 0.000
#&gt; SRR1975501     1  0.0162     0.8227 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1975502     1  0.0162     0.8227 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1975499     4  0.0404     0.9158 0.000 0.012 0.000 0.988 0.000
#&gt; SRR1975500     4  0.0404     0.9158 0.000 0.012 0.000 0.988 0.000
#&gt; SRR1975497     1  0.3949     0.4449 0.696 0.000 0.000 0.300 0.004
#&gt; SRR1975498     1  0.3949     0.4449 0.696 0.000 0.000 0.300 0.004
#&gt; SRR1975493     2  0.3196     0.7692 0.000 0.804 0.000 0.004 0.192
#&gt; SRR1975494     2  0.3196     0.7692 0.000 0.804 0.000 0.004 0.192
#&gt; SRR1975495     1  0.1638     0.7725 0.932 0.000 0.000 0.004 0.064
#&gt; SRR1975496     1  0.1638     0.7725 0.932 0.000 0.000 0.004 0.064
#&gt; SRR1975491     4  0.5040     0.5821 0.068 0.272 0.000 0.660 0.000
#&gt; SRR1975492     4  0.5040     0.5821 0.068 0.272 0.000 0.660 0.000
#&gt; SRR1975489     4  0.0162     0.9128 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1975490     4  0.0162     0.9128 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1975487     4  0.0000     0.9143 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975488     4  0.0000     0.9143 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1975485     4  0.0162     0.9128 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1975486     4  0.0162     0.9128 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1975483     1  0.0324     0.8215 0.992 0.000 0.000 0.004 0.004
#&gt; SRR1975484     1  0.0324     0.8215 0.992 0.000 0.000 0.004 0.004
#&gt; SRR1975481     1  0.0162     0.8227 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1975482     1  0.0162     0.8227 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1975477     2  0.1638     0.7808 0.064 0.932 0.000 0.004 0.000
#&gt; SRR1975478     2  0.1638     0.7808 0.064 0.932 0.000 0.004 0.000
#&gt; SRR1975479     4  0.0566     0.9159 0.004 0.012 0.000 0.984 0.000
#&gt; SRR1975480     4  0.0566     0.9159 0.004 0.012 0.000 0.984 0.000
#&gt; SRR1975475     4  0.1741     0.8991 0.024 0.040 0.000 0.936 0.000
#&gt; SRR1975476     4  0.1741     0.8991 0.024 0.040 0.000 0.936 0.000
#&gt; SRR1975473     2  0.1638     0.7808 0.064 0.932 0.000 0.004 0.000
#&gt; SRR1975474     2  0.1638     0.7808 0.064 0.932 0.000 0.004 0.000
#&gt; SRR1975471     1  0.4060     0.1772 0.640 0.000 0.000 0.000 0.360
#&gt; SRR1975472     1  0.4060     0.1772 0.640 0.000 0.000 0.000 0.360
#&gt; SRR1975469     1  0.0162     0.8227 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1975470     1  0.0162     0.8227 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1975467     2  0.5712    -0.0951 0.028 0.488 0.000 0.452 0.032
#&gt; SRR1975468     2  0.5712    -0.0951 0.028 0.488 0.000 0.452 0.032
#&gt; SRR1975465     2  0.3480     0.7569 0.000 0.752 0.000 0.000 0.248
#&gt; SRR1975466     2  0.3480     0.7569 0.000 0.752 0.000 0.000 0.248
#&gt; SRR1975463     2  0.3480     0.7569 0.000 0.752 0.000 0.000 0.248
#&gt; SRR1975464     2  0.3480     0.7569 0.000 0.752 0.000 0.000 0.248
#&gt; SRR1975461     5  0.4000     0.9910 0.228 0.000 0.024 0.000 0.748
#&gt; SRR1975462     5  0.4000     0.9910 0.228 0.000 0.024 0.000 0.748
#&gt; SRR1975459     2  0.3480     0.7569 0.000 0.752 0.000 0.000 0.248
#&gt; SRR1975460     2  0.3480     0.7569 0.000 0.752 0.000 0.000 0.248
#&gt; SRR1975457     2  0.1864     0.7780 0.068 0.924 0.000 0.004 0.004
#&gt; SRR1975458     2  0.1864     0.7780 0.068 0.924 0.000 0.004 0.004
#&gt; SRR1975455     2  0.1638     0.7808 0.064 0.932 0.000 0.004 0.000
#&gt; SRR1975456     2  0.1731     0.7804 0.060 0.932 0.000 0.004 0.004
#&gt; SRR1975453     5  0.3878     0.9909 0.236 0.000 0.016 0.000 0.748
#&gt; SRR1975454     5  0.3878     0.9909 0.236 0.000 0.016 0.000 0.748
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-4-a').click(function(){
  $('#tab-ATC-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-5'>
<p><a id='tab-ATC-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1   p2 p3    p4    p5    p6
#&gt; SRR1975508     3   0.000      1.000 0.000 0.00  1 0.000 0.000 0.000
#&gt; SRR1975507     3   0.000      1.000 0.000 0.00  1 0.000 0.000 0.000
#&gt; SRR1975506     3   0.000      1.000 0.000 0.00  1 0.000 0.000 0.000
#&gt; SRR1975505     3   0.000      1.000 0.000 0.00  1 0.000 0.000 0.000
#&gt; SRR1975503     4   0.256      0.807 0.004 0.00  0 0.840 0.156 0.000
#&gt; SRR1975504     4   0.256      0.807 0.004 0.00  0 0.840 0.156 0.000
#&gt; SRR1975501     1   0.000      0.859 1.000 0.00  0 0.000 0.000 0.000
#&gt; SRR1975502     1   0.000      0.859 1.000 0.00  0 0.000 0.000 0.000
#&gt; SRR1975499     4   0.000      0.900 0.000 0.00  0 1.000 0.000 0.000
#&gt; SRR1975500     4   0.000      0.900 0.000 0.00  0 1.000 0.000 0.000
#&gt; SRR1975497     1   0.348      0.549 0.684 0.00  0 0.316 0.000 0.000
#&gt; SRR1975498     1   0.348      0.549 0.684 0.00  0 0.316 0.000 0.000
#&gt; SRR1975493     2   0.371      0.433 0.000 0.62  0 0.000 0.380 0.000
#&gt; SRR1975494     2   0.371      0.433 0.000 0.62  0 0.000 0.380 0.000
#&gt; SRR1975495     1   0.107      0.839 0.952 0.00  0 0.000 0.000 0.048
#&gt; SRR1975496     1   0.107      0.839 0.952 0.00  0 0.000 0.000 0.048
#&gt; SRR1975491     4   0.422      0.407 0.020 0.00  0 0.592 0.388 0.000
#&gt; SRR1975492     4   0.422      0.407 0.020 0.00  0 0.592 0.388 0.000
#&gt; SRR1975489     4   0.000      0.900 0.000 0.00  0 1.000 0.000 0.000
#&gt; SRR1975490     4   0.000      0.900 0.000 0.00  0 1.000 0.000 0.000
#&gt; SRR1975487     4   0.000      0.900 0.000 0.00  0 1.000 0.000 0.000
#&gt; SRR1975488     4   0.000      0.900 0.000 0.00  0 1.000 0.000 0.000
#&gt; SRR1975485     4   0.000      0.900 0.000 0.00  0 1.000 0.000 0.000
#&gt; SRR1975486     4   0.000      0.900 0.000 0.00  0 1.000 0.000 0.000
#&gt; SRR1975483     1   0.026      0.858 0.992 0.00  0 0.000 0.000 0.008
#&gt; SRR1975484     1   0.026      0.858 0.992 0.00  0 0.000 0.000 0.008
#&gt; SRR1975481     1   0.000      0.859 1.000 0.00  0 0.000 0.000 0.000
#&gt; SRR1975482     1   0.000      0.859 1.000 0.00  0 0.000 0.000 0.000
#&gt; SRR1975477     5   0.000      0.908 0.000 0.00  0 0.000 1.000 0.000
#&gt; SRR1975478     5   0.000      0.908 0.000 0.00  0 0.000 1.000 0.000
#&gt; SRR1975479     4   0.000      0.900 0.000 0.00  0 1.000 0.000 0.000
#&gt; SRR1975480     4   0.000      0.900 0.000 0.00  0 1.000 0.000 0.000
#&gt; SRR1975475     4   0.181      0.862 0.004 0.00  0 0.908 0.088 0.000
#&gt; SRR1975476     4   0.181      0.862 0.004 0.00  0 0.908 0.088 0.000
#&gt; SRR1975473     5   0.000      0.908 0.000 0.00  0 0.000 1.000 0.000
#&gt; SRR1975474     5   0.000      0.908 0.000 0.00  0 0.000 1.000 0.000
#&gt; SRR1975471     1   0.377      0.377 0.596 0.00  0 0.000 0.000 0.404
#&gt; SRR1975472     1   0.377      0.377 0.596 0.00  0 0.000 0.000 0.404
#&gt; SRR1975469     1   0.000      0.859 1.000 0.00  0 0.000 0.000 0.000
#&gt; SRR1975470     1   0.000      0.859 1.000 0.00  0 0.000 0.000 0.000
#&gt; SRR1975467     5   0.516      0.555 0.004 0.16  0 0.200 0.636 0.000
#&gt; SRR1975468     5   0.516      0.555 0.004 0.16  0 0.200 0.636 0.000
#&gt; SRR1975465     2   0.000      0.861 0.000 1.00  0 0.000 0.000 0.000
#&gt; SRR1975466     2   0.000      0.861 0.000 1.00  0 0.000 0.000 0.000
#&gt; SRR1975463     2   0.000      0.861 0.000 1.00  0 0.000 0.000 0.000
#&gt; SRR1975464     2   0.000      0.861 0.000 1.00  0 0.000 0.000 0.000
#&gt; SRR1975461     6   0.000      1.000 0.000 0.00  0 0.000 0.000 1.000
#&gt; SRR1975462     6   0.000      1.000 0.000 0.00  0 0.000 0.000 1.000
#&gt; SRR1975459     2   0.000      0.861 0.000 1.00  0 0.000 0.000 0.000
#&gt; SRR1975460     2   0.000      0.861 0.000 1.00  0 0.000 0.000 0.000
#&gt; SRR1975457     5   0.000      0.908 0.000 0.00  0 0.000 1.000 0.000
#&gt; SRR1975458     5   0.000      0.908 0.000 0.00  0 0.000 1.000 0.000
#&gt; SRR1975455     5   0.000      0.908 0.000 0.00  0 0.000 1.000 0.000
#&gt; SRR1975456     5   0.000      0.908 0.000 0.00  0 0.000 1.000 0.000
#&gt; SRR1975453     6   0.000      1.000 0.000 0.00  0 0.000 0.000 1.000
#&gt; SRR1975454     6   0.000      1.000 0.000 0.00  0 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-5-a').click(function(){
  $('#tab-ATC-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-mclust-signature_compare](figure_cola/ATC-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-mclust-collect-classes](figure_cola/ATC-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "NMF"]
# you can also extract it by
# res = res_list["ATC:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 13917 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-NMF-collect-plots](figure_cola/ATC-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-NMF-select-partition-number](figure_cola/ATC-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.285           0.629       0.736         0.4461 0.532   0.532
#> 3 3 0.871           0.886       0.957         0.4233 0.792   0.624
#> 4 4 0.971           0.937       0.966         0.1543 0.821   0.558
#> 5 5 0.794           0.755       0.854         0.0682 0.958   0.845
#> 6 6 0.757           0.655       0.783         0.0516 0.956   0.813
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-classes'>
<ul>
<li><a href='#tab-ATC-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-NMF-get-classes-1'>
<p><a id='tab-ATC-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1975508     1  0.9775     0.5208 0.588 0.412
#&gt; SRR1975507     1  0.9775     0.5208 0.588 0.412
#&gt; SRR1975506     1  0.9775     0.5208 0.588 0.412
#&gt; SRR1975505     1  0.9775     0.5208 0.588 0.412
#&gt; SRR1975503     1  0.0376     0.7151 0.996 0.004
#&gt; SRR1975504     1  0.0376     0.7151 0.996 0.004
#&gt; SRR1975501     2  0.9754     0.7730 0.408 0.592
#&gt; SRR1975502     2  0.9754     0.7730 0.408 0.592
#&gt; SRR1975499     1  0.4562     0.6361 0.904 0.096
#&gt; SRR1975500     1  0.4690     0.6301 0.900 0.100
#&gt; SRR1975497     2  0.9754     0.7730 0.408 0.592
#&gt; SRR1975498     2  0.9754     0.7730 0.408 0.592
#&gt; SRR1975493     1  0.3584     0.6695 0.932 0.068
#&gt; SRR1975494     1  0.3431     0.6736 0.936 0.064
#&gt; SRR1975495     2  0.9754     0.7730 0.408 0.592
#&gt; SRR1975496     2  0.9754     0.7730 0.408 0.592
#&gt; SRR1975491     1  0.7219     0.4123 0.800 0.200
#&gt; SRR1975492     1  0.7219     0.4123 0.800 0.200
#&gt; SRR1975489     1  0.7453     0.6491 0.788 0.212
#&gt; SRR1975490     1  0.7950     0.6324 0.760 0.240
#&gt; SRR1975487     1  0.1633     0.7222 0.976 0.024
#&gt; SRR1975488     1  0.2043     0.7232 0.968 0.032
#&gt; SRR1975485     1  0.5519     0.7011 0.872 0.128
#&gt; SRR1975486     1  0.8386     0.6195 0.732 0.268
#&gt; SRR1975483     2  0.9732     0.7723 0.404 0.596
#&gt; SRR1975484     2  0.9732     0.7723 0.404 0.596
#&gt; SRR1975481     2  0.9754     0.7730 0.408 0.592
#&gt; SRR1975482     2  0.9754     0.7730 0.408 0.592
#&gt; SRR1975477     1  0.9732     0.5265 0.596 0.404
#&gt; SRR1975478     1  0.9710     0.5294 0.600 0.400
#&gt; SRR1975479     1  0.0938     0.7117 0.988 0.012
#&gt; SRR1975480     1  0.0672     0.7136 0.992 0.008
#&gt; SRR1975475     1  0.2603     0.6911 0.956 0.044
#&gt; SRR1975476     1  0.2603     0.6911 0.956 0.044
#&gt; SRR1975473     1  0.4939     0.7097 0.892 0.108
#&gt; SRR1975474     1  0.4939     0.7097 0.892 0.108
#&gt; SRR1975471     2  0.9732     0.7723 0.404 0.596
#&gt; SRR1975472     2  0.9732     0.7723 0.404 0.596
#&gt; SRR1975469     2  0.9754     0.7730 0.408 0.592
#&gt; SRR1975470     2  0.9754     0.7730 0.408 0.592
#&gt; SRR1975467     1  0.4562     0.6362 0.904 0.096
#&gt; SRR1975468     1  0.4298     0.6467 0.912 0.088
#&gt; SRR1975465     1  0.3431     0.7213 0.936 0.064
#&gt; SRR1975466     1  0.3431     0.7213 0.936 0.064
#&gt; SRR1975463     1  0.4690     0.6299 0.900 0.100
#&gt; SRR1975464     1  0.4298     0.6473 0.912 0.088
#&gt; SRR1975461     2  0.7056     0.2323 0.192 0.808
#&gt; SRR1975462     2  0.7056     0.2323 0.192 0.808
#&gt; SRR1975459     1  0.2948     0.7236 0.948 0.052
#&gt; SRR1975460     1  0.2948     0.7236 0.948 0.052
#&gt; SRR1975457     2  0.8909    -0.0111 0.308 0.692
#&gt; SRR1975458     2  0.8955    -0.0220 0.312 0.688
#&gt; SRR1975455     1  0.9815     0.5134 0.580 0.420
#&gt; SRR1975456     1  0.9815     0.5134 0.580 0.420
#&gt; SRR1975453     2  0.6973     0.6004 0.188 0.812
#&gt; SRR1975454     2  0.6973     0.6004 0.188 0.812
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-1-a').click(function(){
  $('#tab-ATC-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-2'>
<p><a id='tab-ATC-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1975508     3  0.0000     0.8963 0.000 0.000 1.000
#&gt; SRR1975507     3  0.0000     0.8963 0.000 0.000 1.000
#&gt; SRR1975506     3  0.0000     0.8963 0.000 0.000 1.000
#&gt; SRR1975505     3  0.0000     0.8963 0.000 0.000 1.000
#&gt; SRR1975503     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975504     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975501     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975502     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975499     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975500     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975497     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975498     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975493     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975494     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975495     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975496     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975491     2  0.5431     0.6021 0.284 0.716 0.000
#&gt; SRR1975492     2  0.5431     0.6021 0.284 0.716 0.000
#&gt; SRR1975489     3  0.6302     0.0853 0.000 0.480 0.520
#&gt; SRR1975490     3  0.6291     0.1276 0.000 0.468 0.532
#&gt; SRR1975487     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975488     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975485     2  0.2796     0.8552 0.000 0.908 0.092
#&gt; SRR1975486     2  0.3752     0.7963 0.000 0.856 0.144
#&gt; SRR1975483     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975484     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975481     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975482     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975477     2  0.5678     0.5114 0.000 0.684 0.316
#&gt; SRR1975478     2  0.5678     0.5114 0.000 0.684 0.316
#&gt; SRR1975479     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975480     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975475     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975476     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975473     2  0.0424     0.9314 0.000 0.992 0.008
#&gt; SRR1975474     2  0.0424     0.9314 0.000 0.992 0.008
#&gt; SRR1975471     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975472     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975469     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975470     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975467     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975468     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975465     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975466     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975463     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975464     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975461     3  0.0424     0.8908 0.008 0.000 0.992
#&gt; SRR1975462     3  0.0424     0.8908 0.008 0.000 0.992
#&gt; SRR1975459     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975460     2  0.0000     0.9368 0.000 1.000 0.000
#&gt; SRR1975457     3  0.0000     0.8963 0.000 0.000 1.000
#&gt; SRR1975458     3  0.0000     0.8963 0.000 0.000 1.000
#&gt; SRR1975455     3  0.0000     0.8963 0.000 0.000 1.000
#&gt; SRR1975456     3  0.0000     0.8963 0.000 0.000 1.000
#&gt; SRR1975453     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1975454     1  0.0000     1.0000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-2-a').click(function(){
  $('#tab-ATC-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-3'>
<p><a id='tab-ATC-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1975508     3  0.0188      0.992 0.000 0.000 0.996 0.004
#&gt; SRR1975507     3  0.0188      0.992 0.000 0.000 0.996 0.004
#&gt; SRR1975506     3  0.0188      0.992 0.000 0.000 0.996 0.004
#&gt; SRR1975505     3  0.0188      0.992 0.000 0.000 0.996 0.004
#&gt; SRR1975503     2  0.1716      0.935 0.000 0.936 0.000 0.064
#&gt; SRR1975504     2  0.1716      0.935 0.000 0.936 0.000 0.064
#&gt; SRR1975501     1  0.0336      0.991 0.992 0.008 0.000 0.000
#&gt; SRR1975502     1  0.0188      0.995 0.996 0.004 0.000 0.000
#&gt; SRR1975499     2  0.1637      0.938 0.000 0.940 0.000 0.060
#&gt; SRR1975500     2  0.1474      0.942 0.000 0.948 0.000 0.052
#&gt; SRR1975497     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975498     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975493     2  0.1474      0.942 0.000 0.948 0.000 0.052
#&gt; SRR1975494     2  0.1474      0.942 0.000 0.948 0.000 0.052
#&gt; SRR1975495     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975496     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975491     2  0.4466      0.765 0.180 0.784 0.000 0.036
#&gt; SRR1975492     2  0.4418      0.761 0.184 0.784 0.000 0.032
#&gt; SRR1975489     4  0.0000      0.926 0.000 0.000 0.000 1.000
#&gt; SRR1975490     4  0.0000      0.926 0.000 0.000 0.000 1.000
#&gt; SRR1975487     2  0.0657      0.949 0.000 0.984 0.004 0.012
#&gt; SRR1975488     2  0.0657      0.949 0.000 0.984 0.004 0.012
#&gt; SRR1975485     4  0.1637      0.887 0.000 0.060 0.000 0.940
#&gt; SRR1975486     4  0.0921      0.914 0.000 0.028 0.000 0.972
#&gt; SRR1975483     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975484     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975481     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975482     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975477     4  0.0188      0.926 0.000 0.000 0.004 0.996
#&gt; SRR1975478     4  0.0188      0.926 0.000 0.000 0.004 0.996
#&gt; SRR1975479     4  0.0188      0.926 0.000 0.004 0.000 0.996
#&gt; SRR1975480     4  0.0336      0.925 0.000 0.008 0.000 0.992
#&gt; SRR1975475     4  0.4543      0.543 0.000 0.324 0.000 0.676
#&gt; SRR1975476     4  0.4522      0.552 0.000 0.320 0.000 0.680
#&gt; SRR1975473     4  0.0188      0.926 0.000 0.004 0.000 0.996
#&gt; SRR1975474     4  0.0188      0.926 0.000 0.004 0.000 0.996
#&gt; SRR1975471     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975472     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975469     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975470     1  0.0000      0.998 1.000 0.000 0.000 0.000
#&gt; SRR1975467     2  0.0469      0.950 0.000 0.988 0.000 0.012
#&gt; SRR1975468     2  0.0469      0.950 0.000 0.988 0.000 0.012
#&gt; SRR1975465     2  0.0188      0.945 0.000 0.996 0.004 0.000
#&gt; SRR1975466     2  0.0188      0.945 0.000 0.996 0.004 0.000
#&gt; SRR1975463     2  0.0592      0.950 0.000 0.984 0.000 0.016
#&gt; SRR1975464     2  0.0592      0.950 0.000 0.984 0.000 0.016
#&gt; SRR1975461     3  0.0707      0.984 0.000 0.020 0.980 0.000
#&gt; SRR1975462     3  0.0707      0.984 0.000 0.020 0.980 0.000
#&gt; SRR1975459     2  0.0188      0.945 0.000 0.996 0.004 0.000
#&gt; SRR1975460     2  0.0188      0.945 0.000 0.996 0.004 0.000
#&gt; SRR1975457     4  0.0921      0.914 0.000 0.000 0.028 0.972
#&gt; SRR1975458     4  0.0921      0.914 0.000 0.000 0.028 0.972
#&gt; SRR1975455     4  0.1211      0.905 0.000 0.000 0.040 0.960
#&gt; SRR1975456     4  0.1211      0.905 0.000 0.000 0.040 0.960
#&gt; SRR1975453     1  0.0336      0.992 0.992 0.000 0.008 0.000
#&gt; SRR1975454     1  0.0336      0.992 0.992 0.000 0.008 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-3-a').click(function(){
  $('#tab-ATC-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-4'>
<p><a id='tab-ATC-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1975508     3  0.0162      0.967 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1975507     3  0.0162      0.967 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1975506     3  0.0162      0.967 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1975505     3  0.0162      0.967 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1975503     2  0.3266      0.754 0.000 0.796 0.000 0.004 0.200
#&gt; SRR1975504     2  0.3266      0.754 0.000 0.796 0.000 0.004 0.200
#&gt; SRR1975501     1  0.4157      0.718 0.716 0.020 0.000 0.000 0.264
#&gt; SRR1975502     1  0.4157      0.718 0.716 0.020 0.000 0.000 0.264
#&gt; SRR1975499     2  0.4251      0.513 0.000 0.624 0.000 0.004 0.372
#&gt; SRR1975500     2  0.4251      0.513 0.000 0.624 0.000 0.004 0.372
#&gt; SRR1975497     1  0.2074      0.873 0.896 0.000 0.000 0.000 0.104
#&gt; SRR1975498     1  0.2074      0.873 0.896 0.000 0.000 0.000 0.104
#&gt; SRR1975493     2  0.1270      0.835 0.000 0.948 0.000 0.000 0.052
#&gt; SRR1975494     2  0.1270      0.835 0.000 0.948 0.000 0.000 0.052
#&gt; SRR1975495     1  0.1043      0.877 0.960 0.000 0.000 0.000 0.040
#&gt; SRR1975496     1  0.1043      0.877 0.960 0.000 0.000 0.000 0.040
#&gt; SRR1975491     5  0.5073      0.430 0.100 0.212 0.000 0.000 0.688
#&gt; SRR1975492     5  0.5073      0.430 0.100 0.212 0.000 0.000 0.688
#&gt; SRR1975489     4  0.3167      0.726 0.000 0.004 0.004 0.820 0.172
#&gt; SRR1975490     4  0.3167      0.726 0.000 0.004 0.004 0.820 0.172
#&gt; SRR1975487     2  0.3990      0.616 0.000 0.688 0.000 0.004 0.308
#&gt; SRR1975488     2  0.3969      0.626 0.000 0.692 0.004 0.000 0.304
#&gt; SRR1975485     4  0.5216      0.293 0.000 0.040 0.004 0.568 0.388
#&gt; SRR1975486     4  0.5068      0.330 0.000 0.032 0.004 0.580 0.384
#&gt; SRR1975483     1  0.1410      0.884 0.940 0.000 0.000 0.000 0.060
#&gt; SRR1975484     1  0.1410      0.884 0.940 0.000 0.000 0.000 0.060
#&gt; SRR1975481     1  0.2732      0.851 0.840 0.000 0.000 0.000 0.160
#&gt; SRR1975482     1  0.2732      0.851 0.840 0.000 0.000 0.000 0.160
#&gt; SRR1975477     4  0.0162      0.799 0.000 0.004 0.000 0.996 0.000
#&gt; SRR1975478     4  0.0162      0.799 0.000 0.004 0.000 0.996 0.000
#&gt; SRR1975479     4  0.4201      0.545 0.000 0.008 0.000 0.664 0.328
#&gt; SRR1975480     4  0.4201      0.545 0.000 0.008 0.000 0.664 0.328
#&gt; SRR1975475     5  0.6552      0.226 0.000 0.200 0.000 0.388 0.412
#&gt; SRR1975476     5  0.6518      0.206 0.000 0.192 0.000 0.396 0.412
#&gt; SRR1975473     4  0.0290      0.799 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1975474     4  0.0290      0.799 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1975471     1  0.2230      0.850 0.884 0.000 0.000 0.000 0.116
#&gt; SRR1975472     1  0.2230      0.850 0.884 0.000 0.000 0.000 0.116
#&gt; SRR1975469     1  0.1671      0.881 0.924 0.000 0.000 0.000 0.076
#&gt; SRR1975470     1  0.1671      0.881 0.924 0.000 0.000 0.000 0.076
#&gt; SRR1975467     2  0.0865      0.841 0.000 0.972 0.000 0.004 0.024
#&gt; SRR1975468     2  0.0865      0.841 0.000 0.972 0.000 0.004 0.024
#&gt; SRR1975465     2  0.0162      0.840 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1975466     2  0.0162      0.840 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1975463     2  0.0162      0.840 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1975464     2  0.0162      0.840 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1975461     3  0.1952      0.934 0.004 0.000 0.912 0.000 0.084
#&gt; SRR1975462     3  0.1952      0.934 0.004 0.000 0.912 0.000 0.084
#&gt; SRR1975459     2  0.0510      0.836 0.000 0.984 0.000 0.000 0.016
#&gt; SRR1975460     2  0.0510      0.836 0.000 0.984 0.000 0.000 0.016
#&gt; SRR1975457     4  0.0992      0.791 0.000 0.000 0.024 0.968 0.008
#&gt; SRR1975458     4  0.0992      0.791 0.000 0.000 0.024 0.968 0.008
#&gt; SRR1975455     4  0.0794      0.792 0.000 0.000 0.028 0.972 0.000
#&gt; SRR1975456     4  0.0794      0.792 0.000 0.000 0.028 0.972 0.000
#&gt; SRR1975453     1  0.2763      0.831 0.848 0.000 0.004 0.000 0.148
#&gt; SRR1975454     1  0.2763      0.831 0.848 0.000 0.004 0.000 0.148
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-4-a').click(function(){
  $('#tab-ATC-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-5'>
<p><a id='tab-ATC-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1975508     3  0.0146     0.9355 0.000 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1975507     3  0.0146     0.9355 0.000 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1975506     3  0.0146     0.9355 0.000 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1975505     3  0.0291     0.9331 0.000 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1975503     2  0.5477     0.4462 0.000 0.572 0.000 0.316 0.020 0.092
#&gt; SRR1975504     2  0.5477     0.4462 0.000 0.572 0.000 0.316 0.020 0.092
#&gt; SRR1975501     1  0.4095     0.3770 0.512 0.008 0.000 0.000 0.000 0.480
#&gt; SRR1975502     1  0.4095     0.3770 0.512 0.008 0.000 0.000 0.000 0.480
#&gt; SRR1975499     4  0.5753     0.0193 0.000 0.364 0.000 0.460 0.000 0.176
#&gt; SRR1975500     4  0.5753     0.0193 0.000 0.364 0.000 0.460 0.000 0.176
#&gt; SRR1975497     1  0.3432     0.6781 0.764 0.000 0.000 0.020 0.000 0.216
#&gt; SRR1975498     1  0.3432     0.6781 0.764 0.000 0.000 0.020 0.000 0.216
#&gt; SRR1975493     2  0.3012     0.7515 0.000 0.852 0.000 0.104 0.020 0.024
#&gt; SRR1975494     2  0.3012     0.7515 0.000 0.852 0.000 0.104 0.020 0.024
#&gt; SRR1975495     1  0.3003     0.7081 0.812 0.000 0.000 0.016 0.000 0.172
#&gt; SRR1975496     1  0.3003     0.7081 0.812 0.000 0.000 0.016 0.000 0.172
#&gt; SRR1975491     6  0.5513     0.9908 0.056 0.056 0.000 0.288 0.000 0.600
#&gt; SRR1975492     6  0.5459     0.9908 0.056 0.052 0.000 0.288 0.000 0.604
#&gt; SRR1975489     5  0.4344     0.5280 0.000 0.000 0.000 0.336 0.628 0.036
#&gt; SRR1975490     5  0.4344     0.5280 0.000 0.000 0.000 0.336 0.628 0.036
#&gt; SRR1975487     2  0.5152     0.2059 0.000 0.512 0.000 0.400 0.000 0.088
#&gt; SRR1975488     2  0.5146     0.2173 0.000 0.516 0.000 0.396 0.000 0.088
#&gt; SRR1975485     4  0.4139     0.5336 0.004 0.028 0.004 0.736 0.220 0.008
#&gt; SRR1975486     4  0.4273     0.5255 0.004 0.028 0.008 0.728 0.224 0.008
#&gt; SRR1975483     1  0.2357     0.7126 0.872 0.000 0.000 0.012 0.000 0.116
#&gt; SRR1975484     1  0.2357     0.7126 0.872 0.000 0.000 0.012 0.000 0.116
#&gt; SRR1975481     1  0.4282     0.5723 0.656 0.000 0.000 0.040 0.000 0.304
#&gt; SRR1975482     1  0.4282     0.5723 0.656 0.000 0.000 0.040 0.000 0.304
#&gt; SRR1975477     5  0.1116     0.7907 0.000 0.000 0.004 0.028 0.960 0.008
#&gt; SRR1975478     5  0.1116     0.7907 0.000 0.000 0.004 0.028 0.960 0.008
#&gt; SRR1975479     5  0.4808     0.2046 0.000 0.000 0.000 0.468 0.480 0.052
#&gt; SRR1975480     5  0.4808     0.2046 0.000 0.000 0.000 0.468 0.480 0.052
#&gt; SRR1975475     4  0.4549     0.5771 0.000 0.084 0.004 0.736 0.160 0.016
#&gt; SRR1975476     4  0.4549     0.5771 0.000 0.084 0.004 0.736 0.160 0.016
#&gt; SRR1975473     5  0.1138     0.7904 0.000 0.004 0.000 0.024 0.960 0.012
#&gt; SRR1975474     5  0.1138     0.7904 0.000 0.004 0.000 0.024 0.960 0.012
#&gt; SRR1975471     1  0.3744     0.6680 0.756 0.000 0.000 0.044 0.000 0.200
#&gt; SRR1975472     1  0.3744     0.6680 0.756 0.000 0.000 0.044 0.000 0.200
#&gt; SRR1975469     1  0.2680     0.7122 0.860 0.000 0.000 0.032 0.000 0.108
#&gt; SRR1975470     1  0.2680     0.7122 0.860 0.000 0.000 0.032 0.000 0.108
#&gt; SRR1975467     2  0.1967     0.7702 0.000 0.904 0.000 0.084 0.000 0.012
#&gt; SRR1975468     2  0.1967     0.7702 0.000 0.904 0.000 0.084 0.000 0.012
#&gt; SRR1975465     2  0.0000     0.7920 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975466     2  0.0000     0.7920 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1975463     2  0.0551     0.7918 0.000 0.984 0.000 0.004 0.008 0.004
#&gt; SRR1975464     2  0.0551     0.7918 0.000 0.984 0.000 0.004 0.008 0.004
#&gt; SRR1975461     3  0.3080     0.8687 0.008 0.008 0.848 0.024 0.000 0.112
#&gt; SRR1975462     3  0.3080     0.8687 0.008 0.008 0.848 0.024 0.000 0.112
#&gt; SRR1975459     2  0.0260     0.7902 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1975460     2  0.0260     0.7902 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1975457     5  0.1109     0.7820 0.004 0.000 0.016 0.004 0.964 0.012
#&gt; SRR1975458     5  0.1109     0.7820 0.004 0.000 0.016 0.004 0.964 0.012
#&gt; SRR1975455     5  0.0935     0.7814 0.000 0.000 0.032 0.000 0.964 0.004
#&gt; SRR1975456     5  0.0935     0.7814 0.000 0.000 0.032 0.000 0.964 0.004
#&gt; SRR1975453     1  0.4925     0.6214 0.692 0.000 0.040 0.048 0.004 0.216
#&gt; SRR1975454     1  0.4925     0.6214 0.692 0.000 0.040 0.048 0.004 0.216
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-5-a').click(function(){
  $('#tab-ATC-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-NMF-signature_compare](figure_cola/ATC-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-NMF-collect-classes](figure_cola/ATC-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 3.6.0 (2019-04-26)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS:   /usr/lib64/libblas.so.3.4.2
#> LAPACK: /usr/lib64/liblapack.so.3.4.2
#> 
#> locale:
#>  [1] LC_CTYPE=en_GB.UTF-8       LC_NUMERIC=C               LC_TIME=en_GB.UTF-8       
#>  [4] LC_COLLATE=en_GB.UTF-8     LC_MONETARY=en_GB.UTF-8    LC_MESSAGES=en_GB.UTF-8   
#>  [7] LC_PAPER=en_GB.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_GB.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.66.0    ComplexHeatmap_2.3.1 markdown_1.1         knitr_1.26          
#> [5] GetoptLong_0.1.7     cola_1.3.2          
#> 
#> loaded via a namespace (and not attached):
#>  [1] circlize_0.4.8       shape_1.4.4          xfun_0.11            slam_0.1-46         
#>  [5] lattice_0.20-38      splines_3.6.0        colorspace_1.4-1     vctrs_0.2.0         
#>  [9] stats4_3.6.0         blob_1.2.0           XML_3.98-1.20        survival_2.44-1.1   
#> [13] rlang_0.4.2          pillar_1.4.2         DBI_1.0.0            BiocGenerics_0.30.0 
#> [17] bit64_0.9-7          RColorBrewer_1.1-2   matrixStats_0.55.0   stringr_1.4.0       
#> [21] GlobalOptions_0.1.1  evaluate_0.14        memoise_1.1.0        Biobase_2.44.0      
#> [25] IRanges_2.18.3       parallel_3.6.0       AnnotationDbi_1.46.1 highr_0.8           
#> [29] Rcpp_1.0.3           xtable_1.8-4         backports_1.1.5      S4Vectors_0.22.1    
#> [33] annotate_1.62.0      skmeans_0.2-11       bit_1.1-14           microbenchmark_1.4-7
#> [37] brew_1.0-6           impute_1.58.0        rjson_0.2.20         png_0.1-7           
#> [41] digest_0.6.23        stringi_1.4.3        polyclip_1.10-0      clue_0.3-57         
#> [45] tools_3.6.0          bitops_1.0-6         magrittr_1.5         eulerr_6.0.0        
#> [49] RCurl_1.95-4.12      RSQLite_2.1.4        tibble_2.1.3         cluster_2.1.0       
#> [53] crayon_1.3.4         pkgconfig_2.0.3      zeallot_0.1.0        Matrix_1.2-17       
#> [57] xml2_1.2.2           httr_1.4.1           R6_2.4.1             mclust_5.4.5        
#> [61] compiler_3.6.0
```


