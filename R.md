---
permalink: /R
layout: home
title: R Code
---
This page contains supplemental interactive R code for the following project:

<blockquote>Rhoads, S. A. (2021). An executable notebook template to enhance interactivity with research objects. The Journal of XYZ.</blockquote>
<br>

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.css" integrity="sha512-5A8nwdMOWrSz20fDsjczgUidUBR8liPYU+WymTZP1lmY9G6Oc7HlZv156XqnsgNUzTyMefFTcsFH/tnJE/+xBg==" crossorigin="anonymous" />

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.4/require.min.js"></script>

<script type="text/x-thebe-config">
    {
    requestKernel: true,
    binderOptions: {
         repo: "binder-examples/r"
    },
    kernelOptions: {
         name: "R",
         kernelName: "ir",
    }
    }
</script>
<script src="https://unpkg.com/thebe@latest/lib/index.js"></script>
   
<button id="activateButton" style="font-size: 1em;">
    Click here to interact with the code
</button>

<script>
var bootstrapThebe = function() {
   thebelab.bootstrap();
}
document.querySelector("#activateButton").addEventListener('click', bootstrapThebe)
</script>
<br>

## Figure 1

<pre data-executable="true" data-language="r">
x <- 33
print(x)
</pre>