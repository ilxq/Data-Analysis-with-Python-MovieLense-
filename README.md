#代码演示：用Python进行数据分析——以MovieLens电影评分数据集为例
#演示过程见简书http://www.jianshu.com/p/6da523227ace
<br />import pandas as pd
<br />ratings=pd.read_csv('#你的文件路径',header=0)
<br />ratings[0:5]
<br />movies=pd.read_csv('你的文件路径',header=0)
<br />movies[0:5]
data=ratings.merge(movies,on='movieId')
data[0:5]
ratings_by_title=data.groupby('title').size()#评论数大小
ratings_by_title.order(ascending=False)[:10]
active_titles=ratings_by_title.index[ratings_by_title>=10000]
active_titles
mean_ratings=data.pivot_table('rating','title',aggfunc='mean')
mean_ratings=mean_ratings.ix[active_titles]#只对活跃评论的片子进行平均评分排名
mean_ratings.order(ascending=False)
rating_std_by_title=data.groupby('title')['rating'].std()#只考虑分歧最大的片子只需找出得分的方差或标准差
rating_std_by_title=rating_std_by_title.ix[active_titles]#评分量大的片子，过滤
print rating_std_by_title.order(ascending=False)[:10]#降序
#Thanks
