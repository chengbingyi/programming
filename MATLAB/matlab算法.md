# matlab操作
## 目录
- 一、操作使用
- 二、BP神经网络
- 三、RBF、GRNN 和 PNN 神经网络
- 四、竞争神经网络与 SOM 神经网络
- 五、支持向量机
- 六、极限学习机
- 七、决策树与随机森林
- 八、遗传算法
- 九、粒子群优化
- 十、蚁群算法
- 十一、模拟退火算法
- 十二、降维与特征选择
### 引论
* matlab 的作用
### 一、操作使用
#### 1.1 matlab 数据类型
* 数字
* 字符与字符串
* 矩阵
* 元胞数组
* 结构体
#### 1.2 变量规则
注释：% 开头进行注释
	%% ：用于代码分块
```matlab
%% I. 清空环境变量及命令
clear all   % 清除 Workspace 中的所有变量
clc         % 清除Command Window 中的所有命令

%% II. 变量命令规则
%% 
% 1. 变量名区分大小写
A = 3
a = 4

%% 
% 2. 变量名不超过63位
% ABCDEFGHIJKLMNOPQRSTUVWXYZ...（63位） = 3

%%
% 3. 变量名以字母开头，可以由字母、数字和下划线组成，但不能使用标点

%% 
% 4. 变量名应该简洁明了，通过变量名可以直观的看出变量所表示的

%% III. MATLAB 数据类型*
%%
% 1. 数字
2 + 4
...
% 2. 字符与字符串
```
#### 1.3 MATLAB 矩阵操作
* 矩阵的定义与构造
* 矩阵的四则运算
* 矩阵的下标
```matlab
%%
% 3. 矩阵
A = [1 2 3 ; 4 5 6 ; 7 8 9 ]
B = A'    % 矩阵转置
C = A(:)  % 将矩阵转换为列向量
D = inv(A)% 求解逆矩阵
A * D

% 定义三维数组
E = zeros(10,5,3)                 % 包含了三个二维数组
% 分别给每一个二维数组赋值
E(:,:,1) = rand(10,5)
E(:,:,2) = randi(5,10,5)
E(:,:,3) = randn(10,5)

%%
% 4. 元胞数组 (对多维数组的另一种表示方法)
A = cell(1,6)     % 包含六个空矩阵
A{2} = eye(3)     % 给第二个赋值
A{5} = magic(5)   % 给第五个
B = A{5}
% 与三维数组不同，元胞数组中每个数组可以不一样，比如一个是 3X3 的矩阵，另一个是 5X5 的矩阵；而三维数组中每个数组都只能一样，比如一个为二维数组，其他的也为二维

%%
% 5. 结构体
books = struct('name',{{'Machine Learning','Data Mining'}},'price',[30 40])
books.name
books.name(1)
books.name{1}

%% IV. MATLAB 矩阵操作
%%
% 1. 矩阵的定义与构造
A = [1 2 3 4 5 6 7 8 9]  % 直接构造
B = 1:2:9				 % 以 1 开头，以 9 截至，每隔 2 个构造矩阵
C = repmat(B,3,1)        % 复制矩阵
D = ones(2,4)

%%
% 2. 矩阵的四则运算
A = [1 2 3 4 ; 5 6 7 8]
B = [1 1 2 2 ; 2 2 1 1]
C = A + B
D = A - B
E = A * B'      % 两个矩阵相乘必须的一个矩阵行数与第二个矩阵列数相同，eg：2X4 的矩阵必须乘上那个4X2 的矩阵，返回结果为 2X2 的矩阵
F = A .* B      % 对应位置相乘
G = A / B       % B * G = A
% G * B * pinv(B) = A * pinv(B)        G = A * pinv(B)
H = A ./ B      % 同位置相除

%%
% 3. 矩阵的下标
A = magic(5)    % 指定一个5X5的矩阵
B = A(2,3)      % 取出2行3列的一个元素
C = A(3,:)      % 取出整个第三行的元素
D = A(:,4)      % 取出整个第四列的元素
[m,n] = find(A > 20)   % 寻找满足特定条件的元素
```
#### 1.4 MATLAB 逻辑与流程控制
* if ... else ... end
* for ... end
* while ... end
* switch ... case ... end
```matlab
%% V. MATLAB 逻辑与流程控制
%%
% 1. if... else ... end
A = rand(1,10)       % 设置10个随机数 
limit = 0.75;

B = (A > limit);
if any(B)
	fprintf('Indices of values > %4.2f: \n',limit);
	disp(find(B))
else
	disp('All values are below the limit.')
end

%%
% 2. for ... end
k = 10;
hilbert = zeros(k,k);

for m = 1:k
	for n = 1:k
		hilbert(m,n) = 1 / (m + n - 1)
	end
end
hilbert

%%
% 3. while ... end
n = 1;
nFactorial < 1e100
	n = n + 1
	nFactorial = nFactorial * n;
end
n

factorial(69)
factorial(70)

prod(1:69)
prod(1:70)

%%
% 4. switch ... case ... end
mynumber = input('Enter a number:')

switch mynumber
	case -1
		disp('negative one');
	case 0
		disp('zero');
	case 1
		disp('positive one');
	otherwise
		disp('other value');
	end
```
#### 1.5 脚本与函数文件
* 脚本文件
* 函数文件
```matlab
%%
% 1. 脚本文件
myScript.m    % 直接就可以运行

%%
% 2. 函数文件  % 不能直接运行，需要传入参数
mynumber = input('Enter a number:');
output = myFunction(mynumber)
```
#### 1.6 MATLAB 基本绘图操作
* 二维平面绘图
* 三维立体绘图
* 图形的保存与导出
```matlab
%%
% 1. 二维平面绘图   
% 二维平面绘图只需要给定横纵坐标就可以绘制
x = 0:0.01:2*pi;  % 给定 x 轴，0 到 2派，间隔0.01，语法类似 python
y = sin(x);       % 给定 Y 轴
figure			  % 创建一个窗口
plot(x,y)         % 绘制坐标
title('y = sin(x)')  % 给定标题
xlabel('x')		  % 横坐标名称
ylabel('sin(x)')  % 纵坐标名称
xlim([0 2*pi])    % 横坐标范围

x = 0:0.01:20;
y1 = 200*exp(-0.05*x).*sin(x);
y2 = 0.8
```

























































