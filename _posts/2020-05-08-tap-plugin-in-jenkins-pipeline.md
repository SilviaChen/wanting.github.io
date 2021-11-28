---
layout: post
title:  "TAP plugin in Jenkins pipeline"
categories: Software Technical Note
---

1. Add A step for Tap Result in groovy script

    ```
    stage(“Publish TAP results”){
        step([$class: “TapPublisher”, testResults: “*.tap”])
    }
    ```

2. Automatically generate related options at Sidebar Link
   ![Sidebar Link](/assets/images/side_bar.png)

3. Result
   1. TAP result #1
       ![TAP result #1](/assets/images/tap_1.jpeg) 



   2. TAP result #2
       ![TAP result #2](/assets/images/tap_2.png)