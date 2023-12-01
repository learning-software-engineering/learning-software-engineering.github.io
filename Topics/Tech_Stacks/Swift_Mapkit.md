# Introduction to MapKit for SwiftUI

SwiftUI is a very vast collection of features designed by Apple to make iOS development…swift-er. One of those handy features is it’s ability to make maps, specifically with MapKit. 

**Requirements:** To use these MapKit features, you need to use Xcode 15 and later.

## Table of contents
### [What is MapKit?](#what-is-mapkit-1)
### [Creating a map](#creating-a-map-1)
### [Markers](#markers-1)
### [Annotations](#annotations-1)
### [Camera Position](#camera-position-1)
### [Additional Resources](#additional-resources-1)

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
  <img width=1000 src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113125436/15f46149-bc31-4b53-98d5-0e67b44abb26"/>
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

### Customizing your map

**Map Style**
MapKit provides a couple of different map styles, such as `standard`, `imagery`, and `hybrid`. 

<ins>Standard</ins>

The standard style is the default and can be seen in the map we just made. It marks most roads and road names, as well as location markings. Essentially a mini Apple Maps without functionality.

<ins>Imagery</ins>

The imagery style provides a rendered satellite view map. Unlike standard, on imagery roads and locations are not marked.
```swift
import SwiftUI
import MapKit

struct MapContentView: View {
    var body: some View {       
            Map().mapStyle(.imagery)
    }
}

#Preview {
    MapContentView()
}
```
<p align="center">
<img width=1000 src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113125436/a71aecb0-bb55-4031-b395-bf7476dfca83" />
</p>

<ins>Hybrid</ins>

Want rendered satellite view and road/location names? Then the hybrid style is for you! Hybrid combines the view of `imagery` and the road/location naming of `standard`, hence the name hybrid.

```swift
import SwiftUI
import MapKit

struct MapContentView: View {
    var body: some View {       
            Map().mapStyle(.hybrid)
    }
}

#Preview {
    MapContentView()
}
```

<p align="center">
<img width=1000 src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113125436/3bceaf53-b17a-410a-aa1f-43094faad882" />
</p>

**Additional Map Style Features**
You can also add some additional features to the styles:
- `elevation` (hybrid/standard): whether the maps render elevation
- `showsTraffic` (hybrid/standard) : whether the map can display traffic
- `pointsOfInterest` (hybrid/standard) : a collection of certain `PointOfInterestCategories` objects for the map to show
- `emphasis` (standard) : dictates how the app empasizes certain features

For more information, visit [Apple documentation](https://developer.apple.com/documentation/mapkit/mapstyle) for Map Styles. 

## Markers
Now that we have a general map, let’s add Markers. In MapKit, markers are a balloon-shaped annotation that marks a location based on a set of coordinates. 

<p align="center">
<img width=1000 src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113125436/b48b8d6e-78bf-4a47-93ef-4ed82a34758c">
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


### Marker Customization
There are a couple of ways to customize your marker, such as color and what is displayed in the marker bubble.
<p align="center">
<img width=1000 src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113125436/6d12cc84-1e81-4038-a3d0-cac549de6a44" "/>
</p>

**Color**
  
  To change color of your marker you can apply the `.tint()` method. Tint takes in a Color objext so you can either do a systen color such as `.blue` or your own custom color.

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
## Annotations
Annotations allow for MapKit developrs to completely redesign the location coordinate indicators.
Unlike markers which had a set amount of parameters and there was no way to escape the bubble, Annotations instead takes in a Swift UI `View()`.

For example, here we made the annotation to just be a system image with padding rather than a marker bubble.
```swift
import SwiftUI
import MapKit

struct MapContentView: View {
    
    let robarts = CLLocationCoordinate2D(latitude: 43.664486, longitude: -79.399689)
    
    var body: some View {
        Map(){
            Annotation("Robarts", coordinate: robarts){
                Image(systemName: "books.vertical")
                    .padding(6)
                    .foregroundColor(.white)
                    .background(/*@START_MENU_TOKEN@*/.blue/*@END_MENU_TOKEN@*/)
            }
            
        }
    }
}

#Preview {
    MapContentView()
}
```
<p align="center">
<img width=1000 src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113125436/c64ff5e5-8286-4ad4-b24f-3eae8545f247"/>
</p>

Overall, the annotations allow you to make the map pins compeletely your own.

## Camera Position
By default the map focuses on the map contents (markers, annotaions, etc). To focus on a particular location. This can be helpful in a couple cases such as:
 - When you finish searching for a specific location, focus the map on that location
 - Focus the map on the location of the user
 - If the user presses a certain button, change map focus

Using the `MapCameraPosition` we can specify where the user can 


## Additional Resources
MapKit for SwiftUI is very large and has a lot of possible implementations, so this tutorial was just the tip of the ice berg! Below are some additional resources
that could help with your MapKit journey.

**How to...**
- [Enable user location tracking](https://medium.com/@pblanesp/how-to-display-a-map-and-track-the-users-location-in-swiftui-7d288cdb747e)
- [Implement a search bar](https://www.polpiella.dev/mapkit-and-swiftui-searchable-map)

For general information, refer to the [Apple MapKit Documentation](https://developer.apple.com/documentation/mapkit/mapkit_for_appkit_and_uikit). It is very helpful,
but a bit difficult to navigate.
