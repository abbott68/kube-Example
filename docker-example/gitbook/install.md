# 注意事项

## 运行时需要在工作目录中创建 

1. README.md  
2. SUMMARY.md
3. book.json

## 构建镜像jianshu镜像
docker build -t gitbook:v2 .

## 运行容器
docker run -p 4000:4000 -d gitbook:v2 

## 将工作目录挂在到容器中
docker run -p 4000:4000 -v /opt/test:/app  -d gitbook:v2 
