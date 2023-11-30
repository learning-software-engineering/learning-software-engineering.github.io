# Introduction to MapKit for SwiftUI

As mentioned in the sections before, SwiftUI is a very vast collection of features designed by Apple to make iOS development…swift-er. One of those handy features is it’s ability to make maps, specifically with MapKit.

**Requirements:** To use these MapKit features, you need to use Xcode 15 and later.

## Table of contents
### [What is MapKit?](#what-is-mapkit-1)
### [Creating a map](#creating-a-map-1)
### [Markers](#markers-1)

## What is MapKit?
MapKit is one of Apple’s API framework that allows iOS developers to build map-centered views and apps easily and efficiently. 

Based on the [Apple documentation](https://developer.apple.com/documentation/mapkit/), MapKit can:

- Embed maps directly into your app’s windows and views.
- Add annotations and overlays to a map to call out points of interest.
- Add LookAround capabilities to enable users to explore locations at street level.
- Respond to user interactions with well known points of interest, geographical features, and boundaries.
- Provide text completion to make it easy for users to search for a destination or point of interest.
## Creating a Map
Let’s start with a basic map.
<p align="center">
  <img src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113125436/e0292961-e77d-4645-a864-fe3f16d1d9b5"/>
</p>

To create a basic map, you first need to import MapKit into your Swift file. Then simply call Map() in the view. 

```swift
import SwiftUI
import MapKit

struct MapContentView: View {
    var body: some View {       
            Map()
    }
}

#Preview {
    MapContentView()
}
```


Congratulations you made a map! As you can tell this is just the bare bones. Now that you have a map, you have to customize it to fit your needs.


## Markers
Now that we have a general map, let’s add Markers. In MapKit, markers are a balloon-shaped annotation that marks a location based on a set of coordinates. 

<p align="center">
<img src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113125436/b48b8d6e-78bf-4a47-93ef-4ed82a34758c">
</p>

To create a marker, start with a `CLLocationCoordinate2D` object to represent your coordinate. Then, add it to your Map's contents through the `Marker()` class. The example below hardcodes a coordinate for Robarts Library but it still
takes the same approach if you want to set a coordinate dynamically.

  ```swift
  import SwiftUI
  import MapKit
    
  struct MapContentView: View {
     let robarts = CLLocationCoordinate2D(latitude: 43.664486, longitude: -79.399689)
    var body: some View {
             Map(){
                    Marker("Robarts", coordinate: robarts)
                 }
     }
  }
   
   #Preview {
       MapContentView()
}

  ```


**Note:** *By default, the map will automatically frame to fit all markers and annotations. You can change this later on in the Specifying Region section.*

### Marker Customization
There are a couple of ways to customize your marker, such as color and what is displayed in the marker bubble.
<p align="center">
<img src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113125436/6d12cc84-1e81-4038-a3d0-cac549de6a44" "/>
</p>

**Color**
  
  To change color of your marker you can apply the `.tint()` method. Tint takes in a Color objext so you can either do a systen color such as .blue or your own custom color.

  ```swift
     Marker("Robarts", coordinate: robarts).tint(.blue)
  ```

**Icon**

  To change the what is displayed in the Marker bubble you can add the `systemImage`, `image`, or `monogram` parameters to your Marker as shown below.
  ```swift
   \\ System Image
     Marker("Bahen", systemImage: "star.fill", coordinate: bahen)
  
   \\ Image
     Marker("Robarts", image: "<Your Image Name>", coordinate: robarts)
  
   \\ Monogram
     Marker("University College", monogram: Text("UC"), coordinate: uc)
  ```
  
If you want more freedom with your designing map pins, try using [Annotations](#annotations) instead.
### Annotations
Annotations allow for MapKit developrs to completely redesign the location coordinate indicators.
Unlike markers which had a set amount of parameters and there was no way to escape the bubble, Annotations instead take in a `View()`.


### Region
