//
//  MEDIA QUERIES
//––––––––––––––––––––––––––––––––––––––––––––––––––

// A map of breakpoints.
$breakpoints: (
  xs: 576px,
  sm: 769px,
  md: 992px,
  lg: 1200px
);


//
//  RESPOND ABOVE
//––––––––––––––––––––––––––––––––––––––––––––––––––

// @include respond-above(sm) {}
@mixin respond-above($breakpoint) {

  // If the breakpoint exists in the map.
  @if map-has-key($breakpoints, $breakpoint) {

    // Get the breakpoint value.
    $breakpoint-value: map-get($breakpoints, $breakpoint);

    // Write the media query.
    @media (min-width: $breakpoint-value) {
      @content;
    }
  
  // If the breakpoint doesn't exist in the map.
  } @else {

    // Log a warning.
    @warn 'Invalid breakpoint: #{$breakpoint}.';
  }
}


//
//  RESPOND BELOW
//––––––––––––––––––––––––––––––––––––––––––––––––––

// @include respond-below(sm) {}
@mixin respond-below($breakpoint) {

  // If the breakpoint exists in the map.
  @if map-has-key($breakpoints, $breakpoint) {

    // Get the breakpoint value.
    $breakpoint-value: map-get($breakpoints, $breakpoint);

    // Write the media query.
    @media (max-width: ($breakpoint-value - 1)) {
      @content;
    }
  
  // If the breakpoint doesn't exist in the map.
  } @else {

    // Log a warning.
    @warn 'Invalid breakpoint: #{$breakpoint}.';
  }
}


//
//  RESPOND BETWEEN
//––––––––––––––––––––––––––––––––––––––––––––––––––

// @include respond-between(sm, md) {}
@mixin respond-between($lower, $upper) {

  // If both the lower and upper breakpoints exist in the map.
  @if map-has-key($breakpoints, $lower) and map-has-key($breakpoints, $upper) {

    // Get the lower and upper breakpoints.
    $lower-breakpoint: map-get($breakpoints, $lower);
    $upper-breakpoint: map-get($breakpoints, $upper);

    // Write the media query.
    @media (min-width: $lower-breakpoint) and (max-width: ($upper-breakpoint - 1)) {
      @content;
    }
  
  // If one or both of the breakpoints don't exist.
  } @else {

    // If lower breakpoint is invalid.
    @if (map-has-key($breakpoints, $lower) == false) {

      // Log a warning.
      @warn 'Your lower breakpoint was invalid: #{$lower}.';
    }

    // If upper breakpoint is invalid.
    @if (map-has-key($breakpoints, $upper) == false) {

      // Log a warning.
      @warn 'Your upper breakpoint was invalid: #{$upper}.';
    }
  }
}
