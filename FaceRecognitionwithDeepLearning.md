人脸识别是由一系列的几个相关问题组成的：
1. 人脸检测。
2. 对于每一张脸来说，无论光线明暗或面朝别处，它依旧能够识别出是同一个人的脸。
3. 能够在每一张脸上找出可用于与他人区分的独特之处，比如说眼睛有多大，脸有多长等等。
4. 将这张脸的特点与已知的所有人脸进行比较。

也就是说，对于机器学习来说，要想实现人脸识别，是通过将几个算法连接在一起，流水线式的一步步实现的：

# 人脸检测
具体方法：方向梯度直方图（Histogram of Oriented Gradients）方法，简称 HOG. 见论文：Navneet Dalal and Bill Triggs, "Histograms of Oriented Gradients for Human Detection".
要在一张图片中找到脸，我们首先将图像转换为黑白。然后，我们查看图片中的每一个像素，并对单个像素比较与其周围像素的深度。
找到变暗的方向，用箭头标记。
最终每个像素会被一个箭头取代。这些箭头被称为梯度（gradients），它们能显示出图像上从明亮到黑暗的流动过程：
原因：深浅流动不随图片本身的深浅改变。
为了取出最重要的特征，将图片分割，只取每块指向性最强的梯度。
(```)
  import sys
  import dlib
  from skimage import io

  
  file_name = sys.argv[1]

  # Create a HOG face detector using the built-in dlib class
  face_detector = dlib.get_frontal_face_detector()

  win = dlib.image_window()

  # Load the image into an array
  image = io.imread(file_name)

  # Run the HOG face detector on the image data.
  # The result will be the bounding boxes of the faces in our image.
  detected_faces = face_detector(image, 1)

  print("I found {} faces in the file {}".format(len(detected_faces), file_name))

  # Open a window on the desktop showing the image
  win.set_image(image)

  # Loop through each face we found in the image
  for i, face_rect in enumerate(detected_faces):

	# Detected faces are returned as an object with the coordinates 
	# of the top, left, right and bottom edges
	print("- Face #{} found at Left: {} Top: {} Right: {} Bottom: {}".format(i, face_rect.left(), face_rect.top(), face_rect.right(),       face_rect.bottom()))

	# Draw a box around each face we found
	win.add_overlay(face_rect)
	        
  # Wait until the user hits <enter> to close the window	        
  dlib.hit_enter_to_continue()
  
(```)
