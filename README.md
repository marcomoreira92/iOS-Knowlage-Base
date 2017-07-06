# iOS-Knowlage-Base
A small repo where I  save code snippets that helped me develop my apps. 
## 1) iOS
### 1.1)  Animate
``` swift
self.Container.alpha = 0

UIView.animate(withDuration: 0.3, animations: { () -> Void in
        self.Container.alpha = 1

     }, completion: { (finished: Bool) -> Void in

         //TO STUFFF
     })
```


## 2) Watch Kit

### 2.1) Query data from HealtKit (watch OS 3)
```swift
    func getAVGHeartRate(completion:@escaping ((_ avg : Double) -> Void)) {
        
        let typeHeart = HKQuantityType.quantityType(forIdentifier: .heartRate)
        let startDate = Date() - 3 * 24 * 60 * 60 // start date 3 days
        let predicate: NSPredicate? = HKQuery.predicateForSamples(withStart: startDate, end: Date(), options: HKQueryOptions.strictEndDate)
        
        let squery = HKStatisticsQuery(quantityType: typeHeart!, quantitySamplePredicate: predicate, options: .discreteAverage, completionHandler: {(query: HKStatisticsQuery,result: HKStatistics?, error: Error?) -> Void in
            DispatchQueue.main.async(execute: {() -> Void in
                let quantity: HKQuantity? = result?.averageQuantity()
                let beats: Double? = quantity?.doubleValue(for: HKUnit.count().unitDivided(by: HKUnit.minute()))
                print("got: \(String(format: "%.f", beats!))")
                completion(beats!)
            })
            })
        healthStore.execute(squery)
    }
```

### 2.2) Alert 
```swift
let h0 = { print("h0 action")}
let h1 = { print("h1 action")}

let action1 = WKAlertAction(title: "h0 action", style: .default, handler:h0)
let action2 = WKAlertAction(title: "h1 action", style: .default, handler:h0)

self.presentAlert(withTitle: "Title", message: "a message", preferredStyle: .actionSheet, actions: [action1, action2])
   
   ```
