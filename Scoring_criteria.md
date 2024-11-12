## Text complexity
 Value range [0, 1]

 Calculation formula：

$ S = min(1,\frac{T}{\alpha} + \frac{T/N}{\beta}) $

+ T represents the total number of characters on the page  
+ N represents the total number of widgets on the page  
+ α is the coefficient that controls the total number of characters, reflecting the degree of impact that the total amount of text has on complexity    
+ β is the coefficient that controls the average number of characters per widget, reflecting the impact of average character density  

## Image complexity  
Value range [0, 1]

Calculation formula：

$ S = min(1,\frac{P}{10} + \frac{R}{500000}) $

+ P represents the total number of images on the page  
+ R represents the average resolution of each image on the page (e.g., width × height in pixels)  
+ $ \frac{P}{10} $ controls the impact of the number of images on complexity, assuming that 10 images would bring the complexity close to its upper limit  
+ $ \frac{R}{500000} $ controls the impact of image resolution on complexity, assuming that an average resolution of 500,000 pixels (e.g., 1000 × 500 pixels) would bring the complexity to its upper limit  

## Widget complexity  
Value range [0, 1]

Calculation formula：

$ S = min(1,\frac{0.5 \times B + 1 \times T}{10}) $

+ B represents the number of button widgets  
+ T represents the number of text input widgets  
+ The weight of a button is 0.5  
+ The weight of a text input widget is 1  
+ $ \frac{0.5 \times B + 1 \times T}{10} $ calculate the weighted total complexity of the widgets, assuming that 10 is the upper limit control parameter for complexity. When the page contains multiple widgets or the widget types are complex, the score S will approach 1  

## Total score for a single step  
$ S_{\text{Total score for a single step}} = S_{\text{Text complexity}} + S_{\text{Image complexity}} + S_{\text{Widget complexity}} $

## Total score for a single scenario  
$ 
S_{\text{Total score for a single scenario}} = \left( \sum_{i=1}^{n} S_{\text{Total score for a single step}}(i) \right) \times (\frac{n_{Expected}}{n_{Real}}) $

+ $ n_{Expected} $ represents the total steps required for standard execution  
+ $ n_{real} $represents the total steps of actual execution  

