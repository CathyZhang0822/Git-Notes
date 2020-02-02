## 遇到了html无法显示Image的情况
是因为： The Flask application defaults the files where it attempts to serve static files as the **"static"** path in the root directory for the application.    
所以我们需要在app的根路径下面创建一个static folder，里面创建Images folder。然后路径类似于：   
`<img src="../static/images/3.jpg" alt="New York" width="1100" height="500">`
