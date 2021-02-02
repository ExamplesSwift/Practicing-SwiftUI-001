Example of Addition using SwiftUI

## ViewModel

```
import Foundation

class RutViewModel: ObservableObject {
  
  
  @Published var value1 = "" {
    didSet {
      suming()
    }
  }
  
  @Published var value2 = "" {
    didSet {
      suming()
    }
  }
  
  @Published var sum: Int = 0
  
  func suming() {
    self.sum = (Int(value1) ?? 0) + (Int(value2) ?? 0)
  }
  
  func suming1(_ digA: String, _ digB: String) {
    self.sum = (Int(digA) ?? 0) + (Int(digB) ?? 0)
  }
  
  func suming2(_ digA: String, _ digB: String) -> Int {
    return (Int(value1) ?? 0) + (Int(value2) ?? 0)
  }
  
}
```

## View

```
import SwiftUI

struct RutView: View {
  
  @ObservedObject private var vm = RutViewModel()
  
  var body: some View {
      
    TextField("type value 1 here", text: $vm.value1)
      .keyboardType(.numberPad).padding()
    
    TextField("type value 2 here", text: $vm.value2)
      .keyboardType(.numberPad).padding()
    
    Button(action: {
      vm.suming()
    }, label: {
      Text("Sumar.1..")
    }).padding()
    
    Button(action: {
      vm.suming1(vm.value1, vm.value2)
    }, label: {
      Text("Sumar.2..")
    }).padding()
    
    Button(action: {
      vm.sum = vm.suming2(vm.value1, vm.value2)
    }, label: {
      Text("Sumar.3..")
    }).padding()
    
    
    Text("sum: \(vm.sum)")
    
    Spacer()
    
  }
  
  
}
```

