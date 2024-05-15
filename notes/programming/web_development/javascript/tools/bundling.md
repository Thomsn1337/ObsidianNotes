# Bundling

Organizing code well becomes more important as complexity of the project grows. A project broken down into multiple smaller files, commonly called **modules**, will be easier to maintain and navigate than having to search in a single, long file that is responsible for everything.

The main problem with this approach is that the browser would have to make separate [HTTP requests](../../../software_design_and_principles/http_requests.md) for each file needed. This causes the load time of the page to increase based on how many different files are required, especially on slower networks.

This is where bundlers come into play. They take in a defined file as entry point and creates a dependency graph of of all the dependencies and imported files starting from that point, then combines them into a single output file.

Bundlers will create a **bundle** of the project, containing the source code, but also other assets like [CSS files](../../css/css.md), images, video or audio files. Many bundlers will use different optimization methods to decrease file sizes and thus optimize load times.