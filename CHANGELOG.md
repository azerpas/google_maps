# Change Log

* 0.6.1: 2020-03-08: To better align this crate with Rust conventions, I've
converted many `String` parameters to `&str` parameters. If you're receiving new
compilations errors like `the trait bound google_maps::directions::response::
driving_maneuver::DrivingManeuver: std::convert::From<std::string::String> is
not satisfied` you will have to change your code to borrow the string. For
example, change `TransitCurrency::try_from(currency)` to
`TransitCurrency::try_from(&currency)`.

* 0.6.1: Cleaned up string usage.

* 0.6.1: Added more restrictive `use` examples.

* 0.6.0: 2020-02-29: Cleaned up the `mod` and `use` declarations. To glob import
everything from google_maps into your module, you can use the
`use google_maps::prelude::*` convention now.

* 0.5.2: 2020-02-29: I'm a procedural programmer at heart, so using handles is
second nature to me. In an oversight, I was forcing library users to use
handles without being consciously aware of it. I have improved the ergonomics of
the library. Check out the new examples.

* 0.5.2: 2020-02-29: There were inaccuracies in the rate limiting examples.
Sorry if these poor examples caused you any frustration.

* 0.5.0: 2020-02-23: The `time` crate has deprecated the `PrimitiveDateTime`
struct. This crate has moved from the `time` crate to the `chrono` crate. Since
there is no reasonable way for this crate to always know which time zone is
intended in every context, this crate relies on the `NaiveDateTime` struct. That
means that _time_ and _time zone_ considerations must be tracked and handled by
you, the programmer. Check into the `chrono-tz` crate which integrates nicely
with the `chrono` crate.

* 0.4.6: 2020-02-19: Emergency update! Case conflict for TransitMode. Had to
force to lower case in URL query string builder.

* 0.4.6: 2020-02-19: Connected Travis CI.

* 0.4.6: 2020-02-19: Added support for sub-steps in Directions API.

* 0.4.5: 2020-02-19: Emergency update! Custom deserializer for Durations was
not included in the 0.4.4 release.

* 0.4.4: 2020-02-19: Interface should be stablizing.

* 0.4.4: Added some helper functions for destructuring responses.

* 0.4.4: Ensured response structures are all declared as public.

* 0.4.4: 2020-02-18: Aliased `Distance` and `Duration` structs to
`DirectionsDistance` and `DirectionsDuration` respectively to prevent name
collisions.

* 0.4.4: 2020-02-18: Changed `DirectionsDuration.value` type from `u32` to
`time::Duration` type.

* 0.4.4: 2020-02-18: Dropped my custom Serde deserializer in favour of the
`time` crate's built-in _Serde_ feature.

* 0.4.4: 2020-02-17: Added support for waypoint optimization.

* 0.4.3: 2020-02-09: [Happy 15th birthday to Google
Maps](https://www.blog.google/products/maps/maps-15th-birthday/)!

* 0.4.3: 2020-02-09: Ensured request rate limiting was applied to all API
requests.

* 0.4.2: 2020-02-06: Unix timestamps received from the Google Maps Platform are
now automatically deserialized into `time::PrimitiveDateTime` structs for
convenience.

* 0.4.2: 2020-02-06: Removed precision limit for Google Maps Platform requests.

* 0.4.1: 2020-02-06: Added time zone and currency enumerations for look-up
tables, conversions, and additional handling to be added in the future.

* 0.4.1: 2020-02-06: Fixed some errors in the examples.

* 0.4.1: 2020-02-05: Some internal restructuring to make the library more
consistent. Improved many comments, better documentation.

* 0.4.0: ⚠ **Breaking change**: API keys are no longer passed directly to
Google Maps requests. Now, a structure containing your API key, and several
optional settings, is passed instead. For example:

Before:
```rust
let location = GeocodingReverseRequest::new(
    YOUR_GOOGLE_API_KEY_HERE,
    // 10 Downing St, Westminster, London
    LatLng { lat: 51.5033635, lng: -0.1276248 }
)
```

After. Note to Rust newbies: you may need to change the `?` to an `.unwrap()`
if you're running these examples in your `main()` function.
```rust
let my_settings = ClientSettings::new(YOUR_GOOGLE_API_KEY_HERE);
let location = GeocodingReverseRequest::new(
    &mut my_settings,
    // 10 Downing St, Westminster, London
    LatLng(LatLng::try_from(51.5033635, -0.1276248)?),
)
```

* 0.4.0: ⚠ **Breaking change**: All response structures, such as
`DirectionsResponse`, have been altered.

* 0.4.0: ⚠ **Breaking change**: All LatLng enum variants have had the
{ lat, lng } fields removed in favour of LatLng structs. Use
`LatLng::try_from(lat, lng)` to define latitude/longitude pairs. See the
updated examples.

* 0.4.0: ⚠ **Breaking change**: The Elevation API methods
`positional_request()` & `sampled_path_request()` have been renamed to
`for_positional_request()` & `for_sampled_path_request()` respectively. See the
updated examples.

* 0.4.0: ⚠ **Breaking change**: All `f32` fields have been increased to `f64`
fields.

* 0.4.0: Implemented automatic retry with exponential backoff. This client
library will now attempt to query the Google Cloud Platform several times before
giving up and returning an error. Temporary network hiccups will no longer cause
your program to fail.

* 0.4.0: Implemented request rate limiting. Each API can have different request
rate limits.

* 0.4.0: Now implements the `log` crate with some logging messages for
debugging.