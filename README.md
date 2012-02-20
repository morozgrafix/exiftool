# ExifTool wrapper for ruby

This gem is the simplest thing that could possibly work that
reads the output of ```exiftool``` and renders it into a ruby hash,
with proper "snake-cased" symbols and correctly typed values.

GPS latitude and longitude are rendered as signed floats,
where north and east are positive, and west and south are negative.

Values like shutter speed and exposure time are rendered as Rationals,
which lets the caller show them as fractions (1/250) or as comparable.

## Why not mini_exiftool?

* The values parsed out of mini_exiftool aren't properly numeric
  (things like interop version are "0100", not Integer(100)).
* The GPS values weren't comparable (or easily switched to simple signed floats)
* The library makes the world halt if you don't have exiftool installed
* #to_hash returns CamelCasedKeywords rather than symbols, which is an API change,
  so this isn't just a pull request.
* 44 lines of ruby is better than 339.

## Setup

You'll want to [install ExifTool](http://www.sno.phy.queensu.ca/~phil/exiftool/install.html).

## Usage

```ruby
e = ExifTooler.new("path/to/iPhone 4S.jpg")
e.to_hash
#=>{:make => "Apple", :gps_longitude => -122.47566667, …
e.to_display_hash
#=>{"Make" => "Apple", "GPS Longitude" => -122.47566667, …
e.symbol_display_hash
#=>{:make => "Make", :gps_longitude => "GPS Longitude"}

```
