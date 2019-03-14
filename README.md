# responsive-website-
Finding the Right Responsive Media Queries for All Devices

When defining things such as margins, padding, and font sizes, many of us tend to revert to using the familiar pixels. However, using ems and percentages will make your responsive site easier to manage.

1) so the best practice to code in ems instead of px 

 
2) most important thing is break point 
break point depends on the number of devices we are giving important

here are few common breakpounts we are currenty using this type of media quries 

As you can see, the breakpoints target different screen widths:

Here’s an example. As you can see, the breakpoints target different screen widths:
@media screen and (min-width: 300px) { /* ...mobile styles here... */ }
@media screen and (min-width: 600px) { /* ...tablet styles here... */ }
@media screen and (min-width: 900px) { /* ...desktop styles here...*/ } 


Typical Device Breakpoints

 /* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {...}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {...}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {...}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {...}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {...} 
---------------------------------------------------------------------


i would like to suggest we use breakpoint in em

$bp-small : 24em;
$bp-small-2 : 29.75em;
$bp-small-3 : 39.8em;
$bp-med : 46.8em;
$bp-med-2 : 48em;
$bp-large : 50em;
$bp-large-2 : 54.5em;
$bp-xl : 60em;
$bp-xl-2 : 67em;


@mixin for-phone-only {
  @media (max-width: 599px) { @content; }
}
@mixin for-tablet-portrait-up {
  @media (min-width: 600px) { @content; }
}
@mixin for-tablet-landscape-up {
  @media (min-width: 900px) { @content; }
}
@mixin for-desktop-up {
  @media (min-width: 1200px) { @content; }
}
@mixin for-big-desktop-up {
  @media (min-width: 1800px) { @content; }
}

// usage
.my-box {
  padding: 10px;
  
  @include for-desktop-up {
    padding: 20px;
  }
}

--------------------------second option ---------------------------------

@mixin for-size($range) {
  $phone-upper-boundary: 600px;
  $tablet-portrait-upper-boundary: 900px;
  $tablet-landscape-upper-boundary: 1200px;
  $desktop-upper-boundary: 1800px;

  @if $range == phone-only {
    @media (max-width: #{$phone-upper-boundary - 1}) { @content; }
  } @else if $range == tablet-portrait-up {
    @media (min-width: $phone-upper-boundary) { @content; }
  } @else if $range == tablet-landscape-up {
    @media (min-width: $tablet-portrait-upper-boundary) { @content; }
  } @else if $range == desktop-up {
    @media (min-width: $tablet-landscape-upper-boundary) { @content; }
  } @else if $range == big-desktop-up {
    @media (min-width: $desktop-upper-boundary) { @content; }
  }
}

// usage
.my-box {
  padding: 10px;
  
  @include for-size(desktop-up) {
    padding: 20px;
  }
}


------------------------------point of debate was --------------

to use media quires collectivey 
like 
@media (min-width: 1800px) { @content; }

or

.my-box {
  padding: 10px;
  
  @include for-size(desktop-up) {
    padding: 20px;
  }
}
both will function the same 
difference is 
in first we are using it under @media (min-width: 1800px) { @content; }
collectively and i dont have to search full css it is less scatter 
good for a large css files 
