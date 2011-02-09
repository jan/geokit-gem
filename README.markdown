## NOTES 
----------- Yajl required -------------

I wrote a google geocoder to substitute the current one. The reasons were many. First of all Google has a new V3 Geocoding API which provides json responses (faster than xml ones) and also the old V2 API will be deprecated. The implementation requires Yajl gem as it uses it to parse the json response from Google (I am using the Yajl gem for that and not the regular one because it is faster). Another reason was that using the Geokit gem with ruby 1.9.2 many users complaint for the infamous "incompatible character encodings: UTF-8 and ASCII-8BIT". I have tested this implementation and it doesn't throw any errors. BEWARE! I have wrote no tests so far!

## BENCHMARKS

I have written this benchmark that makes 200 geocoding requests to Google using the old API (xml) and the new API (json):

Benchmark.bm(7) do |x|
    x.report("With Yajl API V3"){ (1..200).each{ Geokit::Geocoders::NGoogleGeocoder.geocode("201 Varick Street, New York") } }
    x.report("With old way"){ (1..200).each{ Geokit::Geocoders::GoogleGeocoder.geocode("201 Varick Street, New York") } } 
end
                               user        system       total              real
With Yajl API V3   0.390000    0.160000   0.550000    ( 90.042886)
With old way        10.050000   0.420000   10.470000   (166.538278)


## GOOGLE GROUP

Follow the Google Group for updates and discussion on Geokit: http://groups.google.com/group/geokit 

## LICENSE

(The MIT License)

Copyright (c) 2007-2009 Andre Lewis and Bill Eisenhauer

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
