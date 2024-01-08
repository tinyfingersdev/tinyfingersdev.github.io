---
layout: post
title:  "Day 24 Project 3 Updates"
categories: swiftui 100days projects
---
The last part of project 3 had us revisit the first 2 projects we worked on, WeSplit and GuessTheFlag game.
I refreshed my memory on how to do these changes by reviewing the previous day's topics. 

In **WeSplit**, our task was to add a conditional text color of red if the user selected a 0% tip. Here's the code
I used to accomplish this by adding the conditional foregroundStyle. All in all, fairly straight forward.

```swift
Section("Total check amount + tip"){
    Text(grandTotal, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
    .foregroundStyle(tipPercentage == 0 ? .red : .black)
}
```

For the **GuessTheFlag** game, we were tasked to create a FlagImage view that included the modifiers
currently in use.  Here's how I did this. I added the following struct:

```swift
struct FlagImage: View {
    var flag: String
    var body: some View {
        Image(flag)
        .clipShape(.capsule)
        .shadow(radius: 5)
    }
}
```

I then used it by replacing the Image with FlagImage when building out the list of flags:

```swift
ForEach(0..<3) { number in
    Button {
        flagtapped(number)
    } label:{
        FlagImage(flag: countries[number])
    }
}
```

The final task was to create a custom ViewModifier to create a large, blue font that could be used to show a
prominent title in a view. Here's how I accomplished this:

```swift
struct BlueHeaderFont: ViewModifier {

    func body(content: Content) -> some View {
        content
        .font(.largeTitle)
        .foregroundColor(.blue)
    }
}

extension View {
    func blueHeader() -> some View {
        modifier(BlueHeaderFont())
    }
}
```

I envoked this custom ViewModifier by chaining the extension as part of Text:

```swift
Text("Hello, world!")
.blueHeader()
```

Here's the final result of the custom view modifier:

![large blue header text](/assets/images/custom-view-modifier.png)