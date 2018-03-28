# Let's Build: With Ruby On Rails - Blog With Comments

## 案例分析：

### 构建 demo_blog 的案例的关键在于完成三个维度的动作：

- （1） gem 安装和调试；
- （2） 增删改查 的功能的调试 + 样式 的调试；
- （3） 评论功能 的调试；

```
cd workspace
rails new demo_blog
ls
cd demo_blog
ls
git init
git status
git add .
git commit -m "initial commit"
rails server
git remote add origin https://github.com/shenzhoudance/demo_blog.git
git push -u origin master
```
![image](https://ws4.sinaimg.cn/large/006tNc79gy1fpre75f7c0j317w0me0yi.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpre47c21ej31040y0az2.jpg)

```
git checkout -b gem
https://rubygems.org/
gem 'better_errors', '~> 2.4'
gem 'bulma-rails', '~> 0.6.2'
gem 'simple_form', '~> 3.5', '>= 3.5.1'
---
group :development do
---
gem 'guard', '~> 2.14', '>= 2.14.2'
gem 'guard-livereload', '~> 2.5', '>= 2.5.2'
---
bundle install
git add .
git commit -m "add gems"
```
https://bulma.io/documentation/overview/start/
https://github.com/guard/guard-livereload
http://livereload.com/extensions/
```
rails generate simple_form:install
gem 'guard-livereload', '~> 2.5', '>= 2.5.2', require: false
bundle
rails s
bundle exec guard
exit
```
![image](https://ws2.sinaimg.cn/large/006tNc79ly1fpsbhgsktij313207wmza.jpg)
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsbfs8wjmj31kw0p87d6.jpg)
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsbgpxuv6j31hw0rq45t.jpg)
```
git status
git add .
git commit -m "add gems"
git push origin gem
```
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsbjx835fj31b80vgjyp.jpg)

# Github 上传方法

![image](https://ws3.sinaimg.cn/large/006tNc79ly1fpsbmo5v3bj31kw0rx0zk.jpg)
![image](https://ws3.sinaimg.cn/large/006tNc79ly1fpsbmjwlqgj31800qydjc.jpg)
![image](https://ws3.sinaimg.cn/large/006tNc79ly1fpsbmfh6rxj31960sgjx2.jpg)
![image](https://ws2.sinaimg.cn/large/006tNc79ly1fpsbm8x3bvj318w0sktee.jpg)
```
rails g controller --help
```
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsbu2iq0rj314k10sagy.jpg)

```
git checkout -b posts
---
rails g controller posts

rails g model Post title:string content:text
rake db:migrate

recources :posts
root 'posts#index'

index.html.erb
show.html.erb
new.html.erb
edit.html.erb
_form.html.erb

---
app/assets/stylesheets/application.scss
@import "bulma";
```
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsd0phf70j30v009qaar.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsd17beltj30ic07674n.jpg)

```
app/controllers/posts_controller.rb
---
class PostsController < ApplicationController
   def index
     @post = Post.all.order("created_at DESC")
  end

  def new
    @post = Post.new
  end

  def create
    @post = Post.new(post_params)

    if @post.save
      redirect_to @post
    else
      render 'new'
    end
  end

  def show
    @post = Post.find(params[:id])
end

 def update
   @post = Post.find(params[:id])

   if @post.update(post_params)
     redirect_to @post
   else
     render 'edit'
   end
 end

 def edit
  @post = Post.find(params[:id])
 end

 def destroy
   @post = Post.find(params[:id])
   @post.destroy
   redirect_to root_path
 end

  private

  def post_params
    params.require(:post).permit(:title, :content)
 end
end
---
app/views/posts/_form.html.erb
---
<%= simple_form_for @post do |f| %>
<%=f.input :title %>
<%=f.input :content %>
<%=f.button :submit %>
<% end %>
---
app/views/posts/new.html.erb
---
<h1>New Post</h1>
<%= render 'form' %>

---
app/views/posts/show.html.erb
---
<h1><%= @post.title %></h1>
<p><%= @post.content %></p>

<%= link_to "Home", root_path, class: "button" %>
<%= link_to "Edit", edit_post_path(@post), class: "button" %>
<%= link_to "Delete", post_path(@post), method: :delete, data: { confirm: "are you sure? " }, class: "button" %>


---
app/views/posts/index.html.erb
---
<% @post.each do |post| %>
<h1><%= link_to post.title, post %></h1>
<p><%= post.content %><p>
<% end %>

<p><%= link_to "New Post", new_post_path %><p>

```
# post 的最终效果
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsipe1f85j30s20acq41.jpg)
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsiorwjcbj30p60ckdgk.jpg)
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsip5qecsj30u00aw0tx.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79ly1fpsip0wzz9j30p80by75d.jpg)

```
git status
git add .
git commit -m "add post CRUD"
git push origin posts
