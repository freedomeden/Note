

###Android中bitmap获取像素的RGB

对图片的特定位置取色，比如类似与吸管效果。取色后如何获取其R、G、B、A 代码如下：


```java    
	int color = bitmap.getPixel(x, y);//x、y为bitmap所对应的位置
	int r = Color.red(color);
	int g = Color.green(color);
	int b = Color.blue(color);
	int a = Color.alpha(color);
```

如果要把R、G、B、A转为16进制（比如转为16进制命令发送等等），RGB转为16进制代码如下：
    
```java
	String r1=Integer.toHexString(r);
	String g1=Integer.toHexString(g);
	String b1=Integer.toHexString(b);
	String colorStr=r1+g1+b1;    //十六进制的颜色字符串。
```

### Bitmap类getPixels()详解

```java
void getPixels (int[] pixels, 
                int offset, 
                int stride, 
                int x, 
                int y, 
                int width, 
                int height)
```

getPixels()函数把一张图片，从指定的偏移位置（offset），指定的位置（x,y）截取指定的宽高（width,height ），把所得图像的每个像素颜色转为int值，存入pixels。

stride 参数指定在行之间跳过的像素的数目。图片是二维的，存入一个一维数组中，那么就需要这个参数来指定多少个像素换一行。

#####stride参数两种用处

>第一种: 可以截取图片中部分区域或者图片拼接

* 1.1、截图：
  * 假设读取像素值的原图片宽为w,高为h,此时设置参数pixels[w* h], 参数stride为 w ,参数offset为0，参数x ,y为截图的起点位置，参数width和height为截图的宽度和高度，

  * 则此方法运行后，返回的pixels[]数组中从pixels[0]至pixels[width*height-1]里存储的是从图片( x , y )处起读取的截图大小为width * height的像素值．


	//截取图片
	mBitmap2.getPixels(pixels, 0, w, 50, 0, w/2, h/2);  
	mBitmap3 = Bitmap.createBitmap(pixels, 0, w, w, h,Bitmap.Config.ARGB_8888);  
	mBitmap4 =Bitmap.createBitmap(pixels, 0, w, w, h,Bitmap.Config.ARGB_4444);
* 1.2、改变offset
  * 下面设置下getPixels()方法中offset，使得黄色部分截图出现在它在原图中的位置， offset = x + y*w ，本例代码如下：

  * 显示在右上角 offset = 50 + 0* 100

	mBitmap2.getPixels(pixels, 50, w, 50, 0, w/2, h/2);
* 显示在右下角 offset = 50 + 50* 100

  mBitmap2.getPixels(pixels, 5050, w, 50, 0, w/2, h/2);

* getPixels()是把二维的图片的每一行像素颜色值读取到一个一维数组中offset指明了所截取的图片的第一个像素的起始位置，如果显示在右下角，起始坐标是（50,50），这个点就是第50行，再移动50个像素，每行100个像素，所以在一维数组中的位置就是50+50*100

* 1.3、改变stride
  * 先给出stride的结论，

  * 在原图上截取的时候，需要读取stride个像素再去读原图的下一行
    如果一行的像素个数足够，就读取stride个像素再下一行读
    如果一行的像素个数不够，用0（透明）来填充到 stride个
    得到的数据，依次存入pixels[]这个一维数组中

```
mBitmap2.getPixels(pixels, 0, w/2, 50, 0, w/2, h/2);
```



* stride 设为宽度的一半，上面的代码在截取原图的时候就是从（50,0）的位置读取一半然后换行，一直这样，直到读取够指定的宽高（w/2, h/2），把这些数据存储到pixels[]中，所以在pixels[]的前2500个整数存储的是黄色区块的信息。

* stride 设为宽度的2倍，上面的代码在截取原图的时候就是从（50,0）的位置读取2w个像素然后换行，但是指定读取的宽度为w/2，所以剩下的w3/2个值用0填充。一直这样，直到读取够指定的宽高（w/2, h/2），把这些数据存储到pixels[]中，所以在pixels[]中存储的是{ w/2个黄色区块信息，w3/2个透明值 ，w/2个黄色区块信息，w3/2个透明值 ，……..}，所以看到左边的黄色，感觉颜色变淡了，就是因为有透明颜色参杂进来

* 另，pixels.length >= stride * height,否则会抛出ArrayIndexOutOfBoundsException　异常

  ​

  图片拼接

* 假设两张图片大小都为 w * h ，getPixels()方法中设置参数pixels[2*w*h],参数offset = 0，stride = 2*w读取第一张图片，再次运行getPixels()方法，设置参数offset = w，stride = 2*w，读取第二张图片，再将pixels[]绘制到画布上就可以看到两张图片已经拼接起来了．

> 第二种:

* stride表示数组pixels[]中存储的图片每行的数据，在其中可以附加信息，即 stride = width + padding，