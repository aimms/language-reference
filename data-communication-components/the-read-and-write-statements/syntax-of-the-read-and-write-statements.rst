.. _sec:rw.read-write:

Syntax of the ``READ`` and ``WRITE`` Statements
===============================================

.. _read:

.. _write:

.. rubric:: ``READ`` and ``WRITE`` statements

In ``READ`` and ``WRITE`` statement you can specify the data source
type, what data will be transferred, and in what mode. The syntax of the
statements reflect these aspects.

.. _read-write-statement:

.. rubric:: Syntax

*read-write-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 653.20266 627.19519"
	   height="627.19519"
	   width="653.20264"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,3640.2739)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><g
	         transform="scale(1.65644)"
	         id="g14"><path
	           id="path16"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 54.3333,16300 -12.074,-30.2 h 24.1481" /></g><g
	         transform="scale(1.63926)"
	         id="g18"><path
	           id="path20"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 170.808,16287.8 -30.501,12.2 v -24.4" /></g><g
	         transform="scale(10)"
	         id="g22"><text
	           id="text26"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,33,2666)"><tspan
	             id="tspan24"
	             y="0"
	             x="0">WRITE</tspan></text>
	</g><g
	         transform="scale(1.63926)"
	         id="g28"><path
	           id="path30"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 451.422,16287.8 30.502,-12.2 v 24.4" /></g><g
	         transform="scale(1.65644)"
	         id="g32"><path
	           id="path34"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 561.444,16300 -12.074,-30.2 h 24.149" /></g><g
	         transform="scale(1.65767)"
	         id="g36"><path
	           id="path38"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 190.629,16287.9 -30.163,12.1 v -24.1" /></g><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,36.6,2696)"><tspan
	             id="tspan42"
	             y="0"
	             x="0">READ</tspan></text>
	</g><g
	         transform="scale(1.65767)"
	         id="g46"><path
	           id="path48"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 424.693,16287.9 30.163,-12 v 24.1" /></g><g
	         transform="scale(1.65767)"
	         id="g50"><path
	           id="path52"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 669.615,16287.9 -30.163,12.1 v -24.1" /></g><g
	         transform="scale(10)"
	         id="g54"><text
	           id="text58"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,116,2696)"><tspan
	             id="tspan56"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/the-read-and-write-statements/syntax-of-the-read-and-write-statements.html#selection">selection</a></tspan></text>
	</g><g
	         transform="scale(1.65767)"
	         id="g60"><path
	           id="path62"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1015.59,16287.9 30.17,-12 v 24.1" /></g><g
	         transform="scale(1.65951)"
	         id="g64"><path
	           id="path66"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 614.64,16269.9 12.051,30.1 h -24.103" /></g><g
	         transform="scale(1.65951)"
	         id="g68"><path
	           id="path70"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1068.7,16269.9 12.05,30.1 h -24.1" /></g><g
	         transform="scale(1.65767)"
	         id="g72"><path
	           id="path74"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1178.47,16287.9 -30.16,12.1 v -24.1" /></g><g
	         transform="scale(10)"
	         id="g76"><text
	           id="text80"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,200.352,2696)"><tspan
	             id="tspan78"
	             y="0"
	             x="0">FROM</tspan></text>
	</g><g
	         transform="scale(1.65767)"
	         id="g82"><path
	           id="path84"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1412.54,16287.9 30.16,-12 v 24.1" /></g><g
	         transform="scale(1.65644)"
	         id="g86"><path
	           id="path88"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1125.01,16300 -12.07,-30.2 h 24.15" /></g><g
	         transform="scale(1.63926)"
	         id="g90"><path
	           id="path92"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1235.63,16287.8 -30.5,12.2 v -24.4" /></g><g
	         transform="scale(10)"
	         id="g94"><text
	           id="text98"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,207.552,2666)"><tspan
	             id="tspan96"
	             y="0"
	             x="0">TO</tspan></text>
	</g><g
	         transform="scale(1.63926)"
	         id="g100"><path
	           id="path102"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1384.47,16287.8 30.51,-12.2 v 24.4" /></g><g
	         transform="scale(1.65644)"
	         id="g104"><path
	           id="path106"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1467.92,16300 -12.08,-30.2 h 24.15" /></g><g
	         transform="scale(1.65644)"
	         id="g108"><path
	           id="path110"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1522.25,16300 -12.07,-30.2 h 24.14" /></g><g
	         transform="scale(1.63926)"
	         id="g112"><path
	           id="path114"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1654.11,16287.8 -30.5,12.2 v -24.4" /></g><g
	         transform="scale(10)"
	         id="g116"><text
	           id="text120"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,276.152,2666)"><tspan
	             id="tspan118"
	             y="0"
	             x="0">FILE</tspan></text>
	</g><g
	         transform="scale(1.63926)"
	         id="g122"><path
	           id="path124"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1890.8,16287.8 30.5,-12.2 v 24.4" /></g><g
	         transform="scale(1.65644)"
	         id="g126"><path
	           id="path128"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1985.9,16300 -12.08,-30.2 h 24.15" /></g><g
	         transform="scale(1.65767)"
	         id="g130"><path
	           id="path132"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1614.03,16287.9 -30.17,12.1 v -24.1" /></g><g
	         transform="scale(10)"
	         id="g134"><text
	           id="text138"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,272.552,2696)"><tspan
	             id="tspan136"
	             y="0"
	             x="0">TABLE</tspan></text>
	</g><g
	         transform="scale(1.65767)"
	         id="g140"><path
	           id="path142"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1891.52,16287.9 30.17,-12 v 24.1" /></g><g
	         transform="scale(1.65767)"
	         id="g144"><path
	           id="path146"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2038.72,16287.9 -30.16,12.1 v -24.1" /></g><g
	         transform="scale(10)"
	         id="g148"><text
	           id="text152"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,342.952,2696)"><tspan
	             id="tspan150"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/the-read-and-write-statements/syntax-of-the-read-and-write-statements.html#data-source">data-source</a></tspan></text>
	</g><g
	         transform="scale(1.65767)"
	         id="g154"><path
	           id="path156"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2481.27,16287.9 30.16,-12 v 24.1" /></g><g
	         transform="scale(1.65644)"
	         id="g158"><path
	           id="path160"
	           style="fill:none;stroke:#000000;stroke-width:2.41480994;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:24.1481, 12.0741;stroke-dashoffset:0;stroke-opacity:1"
	           d="m 2537.44,16300 h 144.89" /></g><g
	         transform="scale(1.58896)"
	         id="g162"><path
	           id="path164"
	           style="fill:none;stroke:#000000;stroke-width:2.51736999;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:25.1737, 12.5869;stroke-dashoffset:0;stroke-opacity:1"
	           d="M 377.606,16300 H 528.649" /></g><g
	         transform="scale(1.59018)"
	         id="g166"><path
	           id="path168"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 641.435,16287.4 -31.443,12.6 v -25.2" /></g><g
	         transform="scale(10)"
	         id="g170"><text
	           id="text174"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,107,2586)"><tspan
	             id="tspan172"
	             y="0"
	             x="0">IN</tspan></text>
	</g><g
	         transform="scale(1.59018)"
	         id="g176"><path
	           id="path178"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 794.877,16287.4 31.442,-12.6 v 25.2" /></g><g
	         transform="scale(1.59018)"
	         id="g180"><path
	           id="path182"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 908.071,16287.4 -31.443,12.6 v -25.2" /></g><g
	         transform="scale(10)"
	         id="g184"><text
	           id="text188"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,149.4,2586)"><tspan
	             id="tspan186"
	             y="0"
	             x="0">DENSE</tspan></text>
	</g><g
	         transform="scale(1.59018)"
	         id="g190"><path
	           id="path192"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1197.35,16287.4 31.44,-12.6 v 25.2" /></g><g
	         transform="scale(1.58896)"
	         id="g194"><path
	           id="path196"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 852.131,16300 -12.587,-31.5 h 25.174" /></g><g
	         transform="scale(1.58896)"
	         id="g198"><path
	           id="path200"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1254.91,16300 -12.59,-31.5 h 25.18" /></g><g
	         transform="scale(1.59018)"
	         id="g202"><path
	           id="path204"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1367.14,16287.4 -31.45,12.6 v -25.2" /></g><g
	         transform="scale(10)"
	         id="g206"><text
	           id="text210"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,222.4,2586)"><tspan
	             id="tspan208"
	             y="0"
	             x="0">REPLACE</tspan></text>
	</g><g
	         transform="scale(1.59018)"
	         id="g212"><path
	           id="path214"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1746.97,16287.4 31.44,-12.6 v 25.2" /></g><g
	         transform="scale(1.58896)"
	         id="g216"><path
	           id="path218"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1804.96,16300 -12.59,-31.5 h 25.17" /></g><g
	         transform="scale(1.58098)"
	         id="g220"><path
	           id="path222"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1896.29,16287.3 -31.63,12.7 v -25.3" /></g><g
	         transform="scale(10)"
	         id="g224"><text
	           id="text228"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,304.8,2571)"><tspan
	             id="tspan226"
	             y="0"
	             x="0">COLUMNS</tspan></text>
	</g><g
	         transform="scale(1.58098)"
	         id="g230"><path
	           id="path232"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2278.33,16287.3 31.63,-12.6 v 25.3" /></g><g
	         transform="scale(1.58896)"
	         id="g234"><path
	           id="path236"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2348.71,16300 -12.59,-31.5 h 25.18" /></g><g
	         transform="scale(1.59202)"
	         id="g238"><path
	           id="path240"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1801.48,16268.6 12.56,31.4 h -25.12" /></g><g
	         transform="scale(1.59939)"
	         id="g242"><path
	           id="path244"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1941.99,16287.5 -31.26,12.5 v -25" /></g><g
	         transform="scale(10)"
	         id="g246"><text
	           id="text250"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,315.6,2601)"><tspan
	             id="tspan248"
	             y="0"
	             x="0">ROWS</tspan></text>
	</g><g
	         transform="scale(1.59939)"
	         id="g252"><path
	           id="path254"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2184.59,16287.5 31.26,-12.5 v 25" /></g><g
	         transform="scale(1.59202)"
	         id="g256"><path
	           id="path258"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2344.18,16268.6 12.57,31.4 h -25.13" /></g><g
	         transform="scale(1.59202)"
	         id="g260"><path
	           id="path262"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1309.03,16268.6 12.56,31.4 h -25.13" /></g><g
	         transform="scale(1.61779)"
	         id="g264"><path
	           id="path266"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="M 1660.91,16287.6 1630,16300 v -24.7" /></g><g
	         transform="scale(10)"
	         id="g268"><text
	           id="text272"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,273.7,2631)"><tspan
	             id="tspan270"
	             y="0"
	             x="0">BACKUP</tspan></text>
	</g><g
	         transform="scale(1.61779)"
	         id="g274"><path
	           id="path276"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1989.75,16287.6 30.91,-12.3 v 24.7" /></g><g
	         transform="scale(1.59202)"
	         id="g278"><path
	           id="path280"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2400.72,16268.6 12.56,31.4 h -25.13" /></g><g
	         transform="scale(1.58896)"
	         id="g282"><path
	           id="path284"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1311.55,16300 -12.58,-31.5 h 25.17" /></g><g
	         transform="scale(1.56258)"
	         id="g286"><path
	           id="path288"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1742.63,16287.2 -31.99,12.8 v -25.6" /></g><g
	         transform="scale(10)"
	         id="g290"><text
	           id="text294"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,277.3,2541)"><tspan
	             id="tspan292"
	             y="0"
	             x="0">MERGE</tspan></text>
	</g><g
	         transform="scale(1.56258)"
	         id="g296"><path
	           id="path298"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2037.02,16287.2 32,-12.8 v 25.6" /></g><g
	         transform="scale(1.58896)"
	         id="g300"><path
	           id="path302"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2405.35,16300 -12.59,-31.5 h 25.18" /></g><g
	         transform="scale(1.58896)"
	         id="g304"><path
	           id="path306"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1311.55,16300 -12.58,-31.5 h 25.17" /></g><g
	         transform="scale(1.54417)"
	         id="g308"><path
	           id="path310"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1740.09,16287 -32.38,13 v -25.9" /></g><g
	         transform="scale(10)"
	         id="g312"><text
	           id="text316"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,273.7,2511)"><tspan
	             id="tspan314"
	             y="0"
	             x="0">INSERT</tspan></text>
	</g><g
	         transform="scale(1.54417)"
	         id="g318"><path
	           id="path320"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2084.61,16287 32.38,-12.9 v 25.9" /></g><g
	         transform="scale(1.58896)"
	         id="g322"><path
	           id="path324"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2405.35,16300 -12.59,-31.5 h 25.18" /></g><g
	         transform="scale(1.59018)"
	         id="g326"><path
	           id="path328"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2460.09,16287.4 -31.44,12.6 v -25.2" /></g><g
	         transform="scale(10)"
	         id="g330"><text
	           id="text334"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,396.2,2586)"><tspan
	             id="tspan332"
	             y="0"
	             x="0">MODE</tspan></text>
	</g><g
	         transform="scale(1.59018)"
	         id="g336"><path
	           id="path338"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2704.09,16287.4 31.44,-12.6 v 25.2" /></g><g
	         transform="scale(1.58896)"
	         id="g340"><path
	           id="path342"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 585.29,16300 -12.587,-31.5 h 25.173" /></g><g
	         transform="scale(1.58896)"
	         id="g344"><path
	           id="path346"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2762.82,16300 -12.59,-31.5 h 25.18" /></g><g
	         transform="scale(1.58896)"
	         id="g348"><path
	           id="path350"
	           style="fill:none;stroke:#000000;stroke-width:2.51736999;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:25.1737, 12.5869;stroke-dashoffset:0;stroke-opacity:1"
	           d="M 2819.46,16300 H 2970.5" /></g><g
	         transform="scale(1.47239)"
	         id="g352"><path
	           id="path354"
	           style="fill:none;stroke:#000000;stroke-width:2.71667004;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:27.1667, 13.5833;stroke-dashoffset:0;stroke-opacity:1"
	           d="m 407.5,16300 h 163" /></g><g
	         transform="scale(1.47239)"
	         id="g356"><path
	           id="path358"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 753.875,16300 -13.583,-34 h 27.166" /></g><g
	         transform="scale(1.45521)"
	         id="g360"><path
	           id="path362"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 893.339,16286.3 -34.359,13.7 v -27.5" /></g><g
	         transform="scale(10)"
	         id="g364"><text
	           id="text368"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,135,2366)"><tspan
	             id="tspan366"
	             y="0"
	             x="0">CHECKING</tspan></text>
	</g><g
	         transform="scale(1.45521)"
	         id="g370"><path
	           id="path372"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1357.88,16286.3 34.35,-13.8 v 27.5" /></g><g
	         transform="scale(1.47239)"
	         id="g374"><path
	           id="path376"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1471.07,16300 -13.58,-34 h 27.17" /></g><g
	         transform="scale(1.47362)"
	         id="g378"><path
	           id="path380"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 857.752,16286.4 -33.93,13.6 v -27.1" /></g><g
	         transform="scale(10)"
	         id="g382"><text
	           id="text386"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,131.4,2396)"><tspan
	             id="tspan384"
	             y="0"
	             x="0">FILTERING</tspan></text>
	</g><g
	         transform="scale(1.47362)"
	         id="g388"><path
	           id="path390"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1365.35,16286.4 33.93,-13.5 v 27.1" /></g><g
	         transform="scale(1.47362)"
	         id="g392"><path
	           id="path394"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1592,16286.4 -33.93,13.6 v -27.1" /></g><g
	         transform="scale(10)"
	         id="g396"><text
	           id="text400"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,239.6,2396)"><tspan
	             id="tspan398"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#binding-tuple">binding-tuple</a></tspan></text>
	</g><g
	         transform="scale(1.47362)"
	         id="g402"><path
	           id="path404"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2126.06,16286.4 33.93,-13.5 v 27.1" /></g><g
	         transform="scale(1.47362)"
	         id="g406"><path
	           id="path408"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2248.21,16286.4 -33.93,13.6 v -27.1" /></g><g
	         transform="scale(10)"
	         id="g410"><text
	           id="text414"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,336.3,2396)"><tspan
	             id="tspan412"
	             y="0"
	             x="0">IN</tspan></text>
	</g><g
	         transform="scale(1.47362)"
	         id="g416"><path
	           id="path418"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2413.78,16286.4 33.93,-13.5 v 27.1" /></g><g
	         transform="scale(1.47362)"
	         id="g420"><path
	           id="path422"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2474.86,16286.4 -33.93,13.6 v -27.1" /></g><g
	         transform="scale(10)"
	         id="g424"><text
	           id="text428"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,369.7,2396)"><tspan
	             id="tspan426"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/identifier-declarations.html#identifier">identifier</a></tspan></text>
	</g><g
	         transform="scale(1.47362)"
	         id="g430"><path
	           id="path432"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2850.45,16286.4 33.93,-13.5 v 27.1" /></g><g
	         transform="scale(1.47239)"
	         id="g434"><path
	           id="path436"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2188.95,16300 -13.58,-34 h 27.17" /></g><g
	         transform="scale(1.47239)"
	         id="g438"><path
	           id="path440"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2913.95,16300 -13.58,-34 h 27.16" /></g><g
	         transform="scale(1.47546)"
	         id="g442"><path
	           id="path444"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1529.01,16266.1 13.56,33.9 h -27.11" /></g><g
	         transform="scale(1.49202)"
	         id="g446"><path
	           id="path448"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2156.96,16286.6 -33.51,13.4 v -26.8" /></g><g
	         transform="scale(10)"
	         id="g450"><text
	           id="text454"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,328.224,2426)"><tspan
	             id="tspan452"
	             y="0"
	             x="0">,</tspan></text>
	</g><g
	         transform="scale(1.49202)"
	         id="g456"><path
	           id="path458"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2291.01,16286.6 33.51,-13.4 v 26.8" /></g><g
	         transform="scale(1.47546)"
	         id="g460"><path
	           id="path462"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2968.89,16266.1 13.56,33.9 h -27.11" /></g><g
	         transform="scale(1.47546)"
	         id="g464"><path
	           id="path466"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 691.31,16266.1 13.555,33.9 h -27.11" /></g><g
	         transform="scale(1.47546)"
	         id="g468"><path
	           id="path470"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 3029.89,16266.1 13.56,33.9 h -27.11" /></g><g
	         transform="scale(1.47239)"
	         id="g472"><path
	           id="path474"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 631.625,16300 -13.583,-34 h 27.166" /></g><g
	         transform="scale(1.47239)"
	         id="g476"><path
	           id="path478"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 3097.33,16300 -13.58,-34 h 27.16" /></g><g
	         transform="scale(1.47239)"
	         id="g480"><path
	           id="path482"
	           style="fill:none;stroke:#000000;stroke-width:2.71667004;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:27.1667, 13.5833;stroke-dashoffset:0;stroke-opacity:1"
	           d="m 3158.45,16300 h 163" /></g><g
	         transform="scale(1.41104)"
	         id="g484"><path
	           id="path486"
	           style="fill:none;stroke:#000000;stroke-width:2.83477998;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:28.3478, 14.1739;stroke-dashoffset:0;stroke-opacity:1"
	           d="M 425.217,16300 H 595.304" /></g><g
	         transform="scale(1.41227)"
	         id="g488"><path
	           id="path490"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 764.726,16285.8 -35.404,14.2 v -28.3" /></g><g
	         transform="scale(10)"
	         id="g492"><text
	           id="text496"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,113,2296)"><tspan
	             id="tspan494"
	             y="0"
	             x="0">WHERE</tspan></text>
	</g><g
	         transform="scale(1.41227)"
	         id="g498"><path
	           id="path500"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1090.44,16285.8 35.41,-14.1 v 28.3" /></g><g
	         transform="scale(1.41227)"
	         id="g502"><path
	           id="path504"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1196.66,16285.8 -35.41,14.2 v -28.3" /></g><g
	         transform="scale(10)"
	         id="g506"><text
	           id="text510"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,174,2296)"><tspan
	             id="tspan508"
	             y="0"
	             x="0">SUFFIX</tspan></text>
	</g><g
	         transform="scale(1.41227)"
	         id="g512"><path
	           id="path514"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1573.35,16285.8 35.41,-14.1 v 28.3" /></g><g
	         transform="scale(1.41104)"
	         id="g516"><path
	           id="path518"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1681.03,16300 -14.18,-35.4 h 28.35" /></g><g
	         transform="scale(1.39386)"
	         id="g520"><path
	           id="path522"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1881.1,16285.7 -35.87,14.3 v -28.7" /></g><g
	         transform="scale(10)"
	         id="g524"><text
	           id="text528"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,268.6,2266)"><tspan
	             id="tspan526"
	             y="0"
	             x="0">=</tspan></text>
	</g><g
	         transform="scale(1.39386)"
	         id="g530"><path
	           id="path532"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2024.59,16285.7 35.87,-14.4 v 28.7" /></g><g
	         transform="scale(1.39386)"
	         id="g534"><path
	           id="path536"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2132.2,16285.7 -35.87,14.3 v -28.7" /></g><g
	         transform="scale(10)"
	         id="g538"><text
	           id="text542"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,302.2,2266)"><tspan
	             id="tspan540"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-element-expressions.html#element-expression">element-expression</a></tspan></text>
	</g><g
	         transform="scale(1.39386)"
	         id="g544"><path
	           id="path546"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2955.09,16285.7 35.87,-14.4 v 28.7" /></g><g
	         transform="scale(1.41104)"
	         id="g548"><path
	           id="path550"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 3096.29,16300 -14.17,-35.4 h 28.35" /></g><g
	         transform="scale(1.41227)"
	         id="g552"><path
	           id="path554"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1935.45,16285.8 -35.4,14.2 v -28.3" /></g><g
	         transform="scale(10)"
	         id="g556"><text
	           id="text560"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,278.338,2296)"><tspan
	             id="tspan558"
	             y="0"
	             x="0">IN</tspan></text>
	</g><g
	         transform="scale(1.41227)"
	         id="g562"><path
	           id="path564"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2108.22,16285.8 35.41,-14.1 v 28.3" /></g><g
	         transform="scale(1.41227)"
	         id="g566"><path
	           id="path568"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2214.44,16285.8 -35.41,14.2 v -28.3" /></g><g
	         transform="scale(10)"
	         id="g570"><text
	           id="text574"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,317.738,2296)"><tspan
	             id="tspan572"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#set-expression">set-expression</a></tspan></text>
	</g><g
	         transform="scale(1.41227)"
	         id="g576"><path
	           id="path578"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2837.72,16285.8 35.4,-14.1 v 28.3" /></g><g
	         transform="scale(1.41411)"
	         id="g580"><path
	           id="path582"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="M 657.657,16264.6 671.8,16300 H 643.514" /></g><g
	         transform="scale(1.41411)"
	         id="g584"><path
	           id="path586"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 3195.65,16264.6 14.14,35.4 h -28.28" /></g><g
	         transform="scale(1.41227)"
	         id="g588"><path
	           id="path590"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 3263.54,16285.8 -35.4,14.2 v -28.3" /></g><g
	         transform="scale(10)"
	         id="g592"><text
	           id="text596"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,467.3,2296)"><tspan
	             id="tspan594"
	             y="0"
	             x="0">;</tspan></text>
	</g><g
	         transform="scale(1.41227)"
	         id="g598"><path
	           id="path600"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 3405.16,16285.8 35.4,-14.1 v 28.3" /></g><g
	         transform="scale(1.41227)"
	         id="g602"><path
	           id="path604"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 3468.89,16285.8 -35.41,14.2 v -28.3" /></g><g
	         transform="scale(1.67485)"
	         id="g606"><path
	           id="path608"
	           style="fill:none;stroke:#000000;stroke-width:2.38827991;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	           d="m 0,16120.9 h 53.7363 m 0,0 v -119.4 c 0,-33 26.7328,-59.7 59.7067,-59.7 v 0 h 53.736 v 0 c 0,32.9 26.733,59.7 59.707,59.7 h 155.239 c 32.974,0 59.706,-26.8 59.706,-59.7 v 0 0 c 0,-33 -26.732,-59.7 -59.706,-59.7 H 226.886 c -32.974,0 -59.707,26.7 -59.707,59.7 v 0 m 274.652,0 h 53.737 v 0 c 32.974,0 59.707,26.7 59.707,59.7 v 119.4 m -501.5387,0 h 59.7067 21.495 53.736 v 0 c 0,33 26.733,59.7 59.707,59.7 H 360.63 c 32.974,0 59.707,-26.7 59.707,-59.7 v 0 0 c 0,-33 -26.733,-59.7 -59.707,-59.7 H 248.381 c -32.974,0 -59.707,26.7 -59.707,59.7 v 0 m 231.663,0 h 53.736 81.202 53.736 m 0,0 v 0 h 53.736 v 59.7 h 342.423 v -59.7 -59.7 H 662.747 v 59.7 m 342.433,0 h 53.73 m -449.899,0 v 119.4 c 0,33 26.733,59.7 59.707,59.7 h 138.375 53.737 138.378 c 32.972,0 59.702,-26.7 59.702,-59.7 v -119.4 h 53.74 m 0,0 v 0 h 53.74 v 0 c 0,33 26.73,59.7 59.7,59.7 h 112.25 c 32.98,0 59.71,-26.7 59.71,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.71,-59.7 h -112.25 c -32.97,0 -59.7,26.7 -59.7,59.7 v 0 m 231.66,0 h 53.74 m -339.14,0 v -119.4 c 0,-33 26.73,-59.7 59.71,-59.7 h -16.72 53.74 v 0 c 0,32.9 26.73,59.7 59.7,59.7 h 26.27 c 32.98,0 59.71,-26.8 59.71,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.71,-59.7 h -26.27 c -32.97,0 -59.7,26.7 -59.7,59.7 v 0 m 145.68,0 h 53.74 -16.72 c 32.97,0 59.71,26.7 59.71,59.7 v 119.4 h 53.73 m 0,0 v -119.4 c 0,-33 26.74,-59.7 59.71,-59.7 v 0 h 53.74 v 0 c 0,32.9 26.73,59.7 59.7,59.7 h 112.25 c 32.98,0 59.71,-26.8 59.71,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.71,-59.7 h -112.25 c -32.97,0 -59.7,26.7 -59.7,59.7 v 0 m 231.66,0 h 53.74 v 0 c 32.97,0 59.7,26.7 59.7,59.7 v 119.4 m -458.55,0 h 59.71 -21.49 53.73 v 0 c 0,33 26.73,59.7 59.71,59.7 h 155.24 c 32.97,0 59.7,-26.7 59.7,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.7,-59.7 h -155.24 c -32.98,0 -59.71,26.7 -59.71,59.7 v 0 m 274.65,0 h 53.74 38.21 53.74 v 59.7 h 438 v -59.7 -59.7 h -438 v 59.7 m 438.01,0 h 53.74 M 501.538,15464.1 h 53.737 m 0,0 v 0 h 53.736 v 0 c 0,33 26.733,59.7 59.707,59.7 h 26.271 c 32.974,0 59.707,-26.7 59.707,-59.7 v 0 0 c 0,-33 -26.733,-59.7 -59.707,-59.7 h -26.271 c -32.974,0 -59.707,26.7 -59.707,59.7 v 0 m 145.685,0 h 53.736 m 0,0 v 0 h 53.736 v 0 c 0,33 26.733,59.7 59.707,59.7 h 155.235 c 32.98,0 59.71,-26.7 59.71,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.71,-59.7 H 921.875 c -32.974,0 -59.707,26.7 -59.707,59.7 v 0 m 274.652,0 h 53.74 m -382.128,0 v -119.4 c 0,-33 26.733,-59.7 59.707,-59.7 h 104.487 53.734 104.49 c 32.97,0 59.71,26.7 59.71,59.7 v 119.4 h 53.73 m 0,0 v 0 h 53.74 v 0 c 0,33 26.73,59.7 59.71,59.7 h 241.21 c 32.98,0 59.71,-26.7 59.71,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.71,-59.7 h -241.21 c -32.98,0 -59.71,26.7 -59.71,59.7 v 0 m 360.63,0 h 53.74 m 0,0 v -29.9 c 0,-32.9 26.73,-59.7 59.7,-59.7 v 0 h 17.91 v 0 c 0,33 26.74,59.7 59.71,59.7 h 241.22 c 32.97,0 59.7,-26.7 59.7,-59.7 v 0 0 c 0,-32.9 -26.73,-59.7 -59.7,-59.7 h -241.22 c -32.97,0 -59.71,26.8 -59.71,59.7 v 0 m 360.63,0 h 17.92 v 0 c 32.97,0 59.7,26.8 59.7,59.7 v 29.9 m -515.86,0 v 29.9 c 0,32.9 26.73,59.7 59.7,59.7 h 64.49 17.91 v 0 c 0,32.9 26.73,59.7 59.71,59.7 h 112.24 c 32.98,0 59.71,-26.8 59.71,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.71,-59.7 h -112.24 c -32.98,0 -59.71,26.7 -59.71,59.7 v 0 m 231.66,0 h 17.91 64.49 c 32.97,0 59.7,-26.8 59.7,-59.7 v -29.9 m -515.86,0 h 59.7 189.27 17.92 248.97 53.74 m -1037.71,0 v 209 c 0,33 26.74,59.7 59.71,59.7 h 246.59 53.74 v 0 c 0,33 26.73,59.7 59.7,59.7 h 198.23 c 32.97,0 59.71,-26.7 59.71,-59.7 v 0 0 c 0,-33 -26.74,-59.7 -59.71,-59.7 h -198.23 c -32.97,0 -59.7,26.7 -59.7,59.7 v 0 m 317.64,0 h 53.73 246.59 c 32.98,0 59.71,-26.7 59.71,-59.7 v -209 m -1037.71,0 v -209 c 0,-32.9 26.74,-59.7 59.71,-59.7 h 268.08 53.74 v 0 c 0,33 26.73,59.7 59.71,59.7 h 155.24 c 32.97,0 59.7,-26.7 59.7,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.7,-59.7 h -155.24 c -32.98,0 -59.71,26.7 -59.71,59.7 v 0 m 274.65,0 h 53.74 268.08 c 32.98,0 59.71,26.8 59.71,59.7 v 209 m -1037.71,0 V 15076 c 0,-33 26.74,-59.7 59.71,-59.7 h 246.59 53.74 v 0 c 0,33 26.73,59.7 59.7,59.7 h 198.23 c 32.97,0 59.71,-26.7 59.71,-59.7 v 0 0 c 0,-33 -26.74,-59.7 -59.71,-59.7 h -198.23 c -32.97,0 -59.7,26.7 -59.7,59.7 v 0 m 317.64,0 h 53.73 246.59 c 32.98,0 59.71,26.7 59.71,59.7 v 388.1 h 53.74 v 0 c 0,33 26.73,59.7 59.7,59.7 h 112.25 c 32.98,0 59.71,-26.7 59.71,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.71,-59.7 h -112.25 c -32.97,0 -59.7,26.7 -59.7,59.7 v 0 m 231.66,0 h 53.74 m -2065.865,0 v -477.7 c 0,-32.9 26.733,-59.7 59.707,-59.7 h 946.358 53.73 946.36 c 32.97,0 59.71,26.8 59.71,59.7 v 477.7 h 53.73 M 501.538,14329.7 h 53.737 m 0,0 v 0 h 53.736 m 0,0 v 0 h 53.736 m 0,0 v -119.4 c 0,-33 26.733,-59.8 59.707,-59.8 v 0 h 53.736 v 0 c 0,33 26.733,59.8 59.707,59.8 H 1120.1 c 32.98,0 59.71,-26.8 59.71,-59.8 v 0 0 c 0,-32.9 -26.73,-59.7 -59.71,-59.7 H 835.897 c -32.974,0 -59.707,26.8 -59.707,59.7 v 0 m 403.62,0 h 53.74 v 0 c 32.97,0 59.7,26.8 59.7,59.8 v 119.4 m -630.503,0 h 59.707 -21.494 53.736 v 0 c 0,32.9 26.733,59.7 59.707,59.7 H 1141.6 c 32.97,0 59.7,-26.8 59.7,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.7,-59.7 H 814.403 c -32.974,0 -59.707,26.7 -59.707,59.7 v 0 m 446.604,0 h 53.74 38.21 53.74 m 0,0 v 0 h 53.74 v 59.7 h 469.88 v -59.7 -59.7 h -469.88 v 59.7 m 469.89,0 h 53.74 m 0,0 v 0 h 53.73 v 0 c 0,32.9 26.73,59.7 59.71,59.7 h 26.27 c 32.97,0 59.71,-26.8 59.71,-59.7 v 0 0 c 0,-33 -26.74,-59.7 -59.71,-59.7 h -26.27 c -32.98,0 -59.71,26.7 -59.71,59.7 v 0 m 145.69,0 h 53.73 v 59.7 h 330.46 v -59.7 -59.7 h -330.46 v 59.7 m 330.47,0 h 53.74 m -637.36,0 v -119.4 c 0,-33 26.73,-59.8 59.7,-59.8 h 232.11 53.73 232.11 c 32.97,0 59.71,26.8 59.71,59.8 v 119.4 h 53.73 m -1268.46,0 v 119.4 c 0,33 26.73,59.7 59.71,59.7 h 461.08 53.73 v 0 c 0,33 26.74,59.7 59.71,59.7 v 0 c 32.98,0 59.71,-26.7 59.71,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.71,-59.7 v 0 c -32.97,0 -59.71,26.7 -59.71,59.7 v 0 m 119.42,0 h 53.73 461.09 c 32.97,0 59.7,-26.7 59.7,-59.7 v -119.4 h 53.74 m -2060.179,0 v 208.9 c 0,33 26.733,59.8 59.707,59.8 h 943.512 53.74 943.51 c 32.98,0 59.71,-26.8 59.71,-59.8 v -208.9 h 53.74 m -2167.655,0 v -209 c 0,-33 26.733,-59.7 59.707,-59.7 h 997.248 53.74 997.25 c 32.97,0 59.71,26.7 59.71,59.7 v 209 h 53.73 M 501.538,13732.6 h 53.737 m 0,0 v 0 h 89.56 v 0 c 0,33 26.733,59.7 59.707,59.7 H 859.78 c 32.974,0 59.707,-26.7 59.707,-59.7 v 0 0 c 0,-33 -26.733,-59.7 -59.707,-59.7 H 704.542 c -32.974,0 -59.707,26.7 -59.707,59.7 v 0 m 274.652,0 h 89.563 v 0 c 0,33 26.73,59.7 59.7,59.7 h 198.23 c 32.98,0 59.71,-26.7 59.71,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.71,-59.7 h -198.23 c -32.97,0 -59.7,26.7 -59.7,59.7 v 0 m 317.64,0 h 89.56 m 0,0 v -119.4 c 0,-33 26.73,-59.7 59.71,-59.7 v 0 h 89.56 v 0 c 0,33 26.73,59.7 59.7,59.7 v 0 c 32.98,0 59.71,-26.7 59.71,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.71,-59.7 v 0 c -32.97,0 -59.7,26.7 -59.7,59.7 v 0 m 119.41,0 h 89.56 v 59.7 h 684.82 v -59.7 -59.7 h -684.82 v 59.7 m 684.84,0 h 89.56 v 0 c 32.97,0 59.71,26.7 59.71,59.7 v 119.4 m -1192.35,0 h 59.71 66.5 89.56 v 0 c 0,33 26.73,59.7 59.71,59.7 H 1718 c 32.97,0 59.7,-26.7 59.7,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.7,-59.7 h -26.27 c -32.98,0 -59.71,26.7 -59.71,59.7 v 0 m 145.68,0 h 89.57 v 59.7 h 525.55 v -59.7 -59.7 h -525.55 v 59.7 m 525.56,0 h 89.56 126.21 89.56 m -2142.885,0 v 119.4 c 0,33 26.733,59.7 59.707,59.7 h 966.958 89.56 966.95 c 32.98,0 59.71,-26.7 59.71,-59.7 v -119.4 h 53.74 v 0 c 0,33 26.73,59.7 59.7,59.7 v 0 c 32.98,0 59.71,-26.7 59.71,-59.7 v 0 0 c 0,-33 -26.73,-59.7 -59.71,-59.7 v 0 c -32.97,0 -59.7,26.7 -59.7,59.7 v 0 m 119.41,0 h 53.74" /></g></g></g></svg></div>

.. _selection:

*selection:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 339.26399 107.2"
	   height="107.2"
	   width="339.26398"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,453.59999)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 360,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,41,296)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#binding-tuple">binding-tuple</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1147,3000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1267,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,131.7,296)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">IN</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1511,3000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1631,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,168.1,296)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/identifier-declarations.html#identifier">identifier</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2184.48,3000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 240,3000 -20,-50 h 40" /><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 848.742,2700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g48"><text
	           id="text52"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,89.8742,266)"><tspan
	             id="tspan50"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/execution-statements/assignment-statements.html#data-selection">data-selection</a></tspan></text>
	</g><path
	         id="path54"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1695.74,2700 50,-20 v 40" /><path
	         id="path56"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2304.48,3000 -20,-50 h 40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,3000 20,50 h -40" /><path
	         id="path60"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1172.24,3300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g62"><text
	           id="text66"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,123.624,326)"><tspan
	             id="tspan64"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1372.24,3300 50,-20 v 40" /><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2424.48,3000 20,50 h -40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2544.48,3000 -50,20 v -40" /><path
	         id="path74"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,3000 h 120 m 0,0 v 0 h 120 m 0,0 v 0 h 120 v 100 h 786.98 V 3000 2900 H 360 v 100 m 787,0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 120 v 100 h 553.46 V 3000 2900 H 1631 v 100 m 553.48,0 h 120 M 240,3000 v -200 c 0,-55.23 44.773,-100 100,-100 h 388.742 120 v 100 H 1695.72 V 2700 2600 H 848.742 v 100 m 846.998,0 h 120 388.74 c 55.23,0 100,44.77 100,100 v 200 h 120 M 120,3000 v 200 c 0,55.23 44.773,100 100,100 h 832.24 120 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 120 832.24 c 55.23,0 100,-44.77 100,-100 v -200 h 120" /></g></g></svg></div>

.. _data-source:

.. rubric:: Data sources

The data source of a ``READ`` or ``WRITE`` statement in AIMMS can be
either

-  a ``File`` represented by either

   -  a ``File`` identifier,

   -  a string constant, or

   -  a scalar string reference,

-  a ``TABLE`` represented by either

   -  a ``DatabaseTable`` identifier,

   -  an element parameter with a range that is a subset of the
      predeclared set :any:`AllDatabaseTables`

Strings for file data sources refer either to an absolute path or to a
relative path. All relative paths are taken relative to the project
directory.

.. rubric:: Examples

Assuming that ``UserSelectedFile`` is a ``File`` identifier, and
``UserFilename`` a string parameter, then the following statements
illustrate the use of strings and ``File`` identifiers.

.. code-block:: aimms

	read from file "C:\Data\Transport\initial.dat" ;
	read from file "data\initial.dat" ;
	read from file UserFileName ;
	read from file UserSelectedFile ;

.. rubric:: Specifying a selection

The *selection* in a ``READ`` or ``WRITE`` statement determines which
data you want to transfer from or to a text file, or database table. A
selection is a list of references to sets, parameters, variables and
constraints. During a ``WRITE`` statement, AIMMS accepts certain
restrictions on each reference to restrict the amount of data written
(as explained below). Note, however, that AIMMS does not accept all
types of restrictions which are syntactically allowed by the syntax
diagram of the ``READ`` and ``WRITE`` statements.

.. rubric:: Default selection

If you do not specify a selection during a ``READ`` statement, AIMMS
will transfer the data of all identifiers stored in the table or file
that can be mapped onto identifiers in your model. If you do not specify
a selection for a ``WRITE`` statement to a text

file, all identifiers declared in your model will be written. When
writing to a database table, AIMMS will write data for all columns in
the table as long as they can be mapped onto AIMMS identifiers.

.. _filtering:

.. _checking:

.. rubric:: Filtering the selection

You can apply the following filtering qualifiers on ``READ`` and
``WRITE`` statements to restrict the data selection:

-  the ``FILTERING`` or ``CHECKING`` clauses restrict the domain of all
   transferred data in both the ``READ`` and ``WRITE`` statements, and

-  an arbitrary logical condition can be imposed on each individual
   parameter and variable in a ``WRITE`` statement.

.. rubric:: ``FILTERING`` versus ``CHECKING``

You can use both the ``FILTERING`` and ``CHECKING`` clause to restrict
the tuples for which data is transferred between a data source and
AIMMS. During a ``WRITE`` statement there is no difference in semantics,
and you can use both clauses interchangeably. During a ``READ``
statement, however, the ``FILTERING`` clause will skip over all data
outside of the filtering domain, whereas the ``CHECKING`` clause will
issue a runtime error when the data source contains data outside of the
filtering domain. This is useful feature for catching typing errors in
text data files.

.. rubric:: Examples

The following examples illustrate filtering and the use of logical
conditions imposed on index domains.

.. code-block:: aimms

	read Distance(i,j) from table RouteTable
	     filtering i in SourceCities, (i,j) in Routes;

	write Transport( (i,j) | Sum(k, Transport(i,k)) > MinimumTransport )
	      to table RouteTable ;

.. rubric:: Advanced filtering on records

If you need more advanced filtering on the records in a database table,
you can use the database to perform this for you. You can

-  define *views* to create temporary tables when the filtering is based
   on a non-parameterized condition, or

-  use *stored procedures* with arguments to create temporary tables
   when the filtering is based on a parameterized condition.

The resulting tables can then be read using a simple form of the
``READ`` statement.

.. _merge:

.. _replace:

.. _backup:

.. _insert:

.. rubric:: Merge, replace or backup mode

| AIMMS allows you to transfer data from and to a file or a database
  table in *merge* mode, *replace* mode or *insert* mode. If you have
  not selected a mode in either a ``READ`` or ``WRITE`` statement, AIMMS
  will transfer the data in replace mode by default, with one exception:
  when reading from a case difference file that was generated by
  :any:`CaseCreateDifferenceFile` function with ``diffTypes`` argument
  equal to ``elementReplacement``, ``elementAddition`` or
  ``elementMultiplication``, the file is always read in merge mode, so
  that the ``diffTypes`` can be applied in a sensible way.
| When you are writing data to a text data file, AIMMS also supports a
  *backup* mode. The *insert* mode can speed up writing to databases.

.. rubric:: Reading in merge mode

When AIMMS reads data in merge mode, it will overwrite existing elements
for all read identifiers, and add new elements as necessary. It is
important to remember that in this mode, if there is no data read for
some of the existing elements, they keep their current value.

.. rubric:: Writing in merge mode

When AIMMS writes data in merge mode, the semantics is dependent on the
type of the data source.

-  If the data source is a text file, AIMMS will *append* the newly
   written data to the end of the file.

-  If the data source is a database table, AIMMS will merge the new values into the existing
   values, creating new records as necessary.

.. rubric:: Reading in replace mode

When AIMMS reads data in replace mode, it will empty the existing data
of all identifiers in the identifier selection, and then read in the new
data.

.. rubric:: Writing in replace mode

When AIMMS writes data in replace mode, the semantics is again dependent
on the type of the data source.

-  If the data source is a text file, AIMMS will *overwrite the entire
   contents* of the file with the newly written data. Thus, if the file
   also contained data for identifiers that are not part of the current
   identifier selection, their data is lost by the ``WRITE`` statement.

-  If the data source is a database table, AIMMS will either empty all
   columns in the table that are mapped onto identifiers in the
   identifier selection (default, ``REPLACE COLUMNS`` mode), or will
   remove all records in the table not written by this write statement
   (``REPLACE ROWS`` mode). The ``REPLACE COLUMNS`` and ``REPLACE ROWS``
   modes are discussed in more detail in :ref:`sec:db.restrictions`).

.. rubric:: Writing in insert mode

Writing in insert mode is only applicable when writing to databases.
Essentially, what it does is writing the selected data to a database
table using SQL *INSERT* statements. In other words, it expects that the
selection of the data that you write to the table doesn't match any
existing primary keys in the database table. If it does, AIMMS will
raise an error message about duplicate keys being written. Functionally,
the insert mode is equivalent to the replace rows mode, with the
non-existing primary keys restriction. Especially when writing to
database tables which already contain a lot of rows, the speed advantage
of the insert mode becomes more visible. 

.. rubric:: Writing in backup mode

When you are transferring data to a text file, AIMMS supports writing in
backup mode in addition to the merge and replace modes. The backup mode
lets you write out files which can serve as a text backup to a (binary)
AIMMS case file. When writing in backup mode, AIMMS

-  skips all identifiers on the identifier list which possess a nonempty
   definition (and, consequently, cannot be read in from a datafile),

-  skips all identifiers for which the property ``NoSave`` has been set,
   and

-  writes the contents of all remaining identifiers in such an order
   that, upon reading the data from the file, all domain sets are read
   before any identifiers defined over such domain sets.

Backup mode is not supported during a ``READ`` statement, or when
writing to a database.

.. rubric:: Writing data in a dense mode

Writing in dense mode is only applicable when writing to databases. Data
in AIMMS is stored for non-default values only, and, by default, AIMMS
only writes these non-default values to a database. In order to write
the default values as well to the database table at hand, you can add
the *dense* keyword before most of the ``WRITE`` modes discussed above.
This will cause AIMMS to write all possible values, including the
defaults, for all tuple combinations considered in the ``WRITE``
statement. Care should be taken that writing in *dense* mode does not
lead to an excessive amount of records being stored in the database. The
mode combination *merge* and *dense* is not allowed, because it is
ambiguous whether or not a non-default entry in the database should be
overwritten by a default value of AIMMS. 
For the same reason, the mode combination *insert* and *dense* is also not allowed.

.. rubric:: Replacing sets

Whenever elements in a domain set have been removed by a ``READ``
statement in replace mode, AIMMS will *not* cleanup all identifiers
defined over that domain. Instead, it will leave it up to you to use the
``CLEANUP`` statement to remove the inactive data that may have been
created.

.. rubric:: Domain filtering

For every ``READ`` and ``WRITE`` statement you can indicate whether or
not you want domain filtering to take place during the data transfer. If
you want domain filtering to be active, you must indicate the list of
indices, or domain conditions to be filtered in either a ``FILTERING``
of ``CHECKING`` clause. In case of ambiguity which index position in a
parameter you want to have filtered you must specify indices in the set
or parameter reference.

.. rubric:: Example

The following ``READ`` statements are not accepted because both
``Routes`` and ``Distance`` are defined over ``Cities`` :math:`\times`
``Cities``, and it is unclear to which position the filtered index ``i``
refers.

.. code-block:: aimms

	read Routes   from table RouteTable filtering i ;
	read Distance from table RouteTable filtering i ;

This ambiguity can be resolved by explicitly adding the relevant indices
as follows.

.. code-block:: aimms

	read (i,j) in Routes from table RouteTable filtering i ;
	read Distance(i,j)   from table RouteTable filtering i ;

.. rubric:: Semantics of domain filtering

When you have activated domain filtering on an index or index tuple,
AIMMS will limit the transfer of data dependent on further index
restrictions.

-  During a ``READ`` statement only the data elements for which the
   value of the given index (tuple) lies within the specified set are
   transfered. If no further index restriction has been specified,
   transfer will take place for all elements of the corresponding domain
   set.

-  During a ``WRITE`` statement only those data elements are transferred
   for which the index (tuple) is contained in the AIMMS set given in
   the (optional) ``IN`` clause. If no set has been specified, and the
   data source is a database table, the transfer is restricted to only
   those tuples that are already present in the table. When the data
   source is a text file

   the latter type of domain filtering is not meaningful and therefore
   ignored by AIMMS.

.. rubric:: ``READ`` example

In the following two ``READ`` statements the data transfer for elements
associated with ``i`` and (``i``,\ ``j``), respectively, is further
restricted through the use of the sets ``SourceCities`` and ``Routes``.

.. code-block:: aimms

	read Distance(i,j) from table RouteTable filtering i in SourceCities ;
	read Distance(i,j) from table RouteTable filtering (i,j) in Routes ;

.. rubric:: ``WRITE`` example

In the following two ``WRITE`` statements, the values of the variable
``Transport(i,j)`` are written to the database table ``RouteTable`` for
those tuples that lie in the AIMMS set ``SelectedRoutes``, or for which
records in the table ``RouteTable`` are already present, respectively.

.. code-block:: aimms

	write Transport(i,j) to table RouteTable filtering (i,j) in SelectedRoutes ;
	write Transport(i,j) to table RouteTable filtering (i,j) ;

The ``FILTERING`` clause in the latter ``WRITE`` statement would have
been ignored by AIMMS when the data source was a text data file.

.. rubric:: Writing selected suffices using the ``WHERE`` clause

Using the ``WHERE`` clause of the ``WRITE`` statement you can instruct
AIMMS, for all identifiers in the identifier selection, to write the
data of either a specified suffix or a set of suffices to file, rather
than their level values. The ``WHERE`` clause can only be specified
during a ``WRITE`` statement to a ``FILE``, and the corresponding set or
element expression must refer to a subset of, or element in, the
predefined set :any:`AllSuffixNames`.

.. rubric:: Example

The following ``WRITE`` statement will write the values of the
:ref:`.Violation` suffix of to the file ``ViolationsReport.txt`` for all
variables in the project.

.. code-block:: aimms

	write AllVariables to file "ViolationsReport.txt" where suffix = 'Violation';
