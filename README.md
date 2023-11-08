# Games101_HomeWork
2023.11.8
今天主要完成了openGL的配置以及实验一的基本功能。

以下是我寻找到关于Windows平台下VS2022的环境配置：https://blog.csdn.net/qq_43419761/article/details/127740207

透视投影矩阵：几个特点：
1.在近平面上的坐标不会发生任何改变
2.在远平面上的坐标z值不会发生改变
3.在中心点的坐标在近远平面上都不会发生改变

自己在作业一中填写的代码部分：
Rotation：
    Eigen::Matrix4f translate;
    translate << cos(rotation_angle), -sin(rotation_angle), 0, 0, sin(rotation_angle), cos(rotation_angle), 0, 0, 0, 0, 1,
        0, 0, 0, 0, 1;

    model = translate * model;
Projection:
Eigen::Matrix4f p;
p << zNear, 0, 0, 0,
    0, zNear, 0, 0,
    0, 0, zNear + zFar, -zNear * zFar,
    0, 0, 1, 0;
float half = eye_fov / 2 * MY_PI / 180;
float top = tan(half) * zNear;
float bottom = -top;
float right = top * aspect_ratio;
float left = -right;
Eigen::Matrix4f m,v;
m << 2 / (right - left), 0, 0, 0,
    0, 2 / (top - bottom), 0, 0,
    0, 0, 2 / (zFar - zNear), 0,
    0, 0, 0, 1;
v << 1, 0, 0, -(right + left) / 2,
    0, 1, 0, -(top + bottom) / 2,
    0, 0, 1, -(zFar + zNear) / 2,
    0, 0, 0, 1;
projection = m * v * p;
实验一图片：
![`ELJWSFH@)`@O25 1G~3RPI](https://github.com/q931326/Games101_HomeWork/assets/124950885/59c1954e-4a20-4e38-ac23-f81fbf93f86b)

