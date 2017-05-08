x1<-"trainResized"                                               // Training dataset
x2<-"testResized"                                                // Test dataset
setwd("C:/Users/Shubha/AppData/Local/Julia-0.3.0")
Y <- read.csv("trainLabels.csv")                                 // Training labels 
 
 library(bmp)                                                    
 img<-read.bmp(file.path(getwd(),x1,"1.bmp"))                    // RGB to Grayscale conversion of "1.bmp"
 r<-0.299*img[,,1]
 g<-0.587*img[,,2]
 b<-0.114*img[,,3]
 img_grayscale<-r+g+b
 image(img_grayscale)
 image(img_grayscale,col=gray.colors(12))


for(i in1:6283)                                                  // Number of training examples is 6283
{img<-read.bmp(file.path(getwd(),x1,paste0(i,".bmp")))           // Reading each bitmap image from the training dataset
if(min(dim(img)==3))                                             // Go for RGB to Grayscale conversion if the image is 3D
{
r<-0.299*img[,,1]                                                // RGB to GrayScale Conversion
g<-0.587*img[,,2]
b<-0.114*img[,,3]
img_grayscale<-r+g+b
}
else
img_grayscale<-img   
X[i,]<-img_grayscale                                             // Stack of all unidimensional images to be stored in 1 big matrix
}

Xtrain<-X[1:as.integer(dim(X)[1]*0.8),] 
Ytrain<-Y[1:as.integer(dim(Y)[1]*0.8),]                          // Splitting the training dataset & labels in the 80:20 data 
dim(Xtrain)
dim(Ytrain)


Xvalidate<-X[as.integer(dim(X)[1]*0.8):6283,]
Yvalidate<-Y[1:as.integer(dim(X)[1]*0.8),] 
dim(Xvalidate)
dim(Yvalidate)