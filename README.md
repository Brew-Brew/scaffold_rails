# Scaffold 로 crud 하기

## 명령어:rails g scaffold Post title:string content:text
+ 위의 명령어로 모든것이 다 해결
+ (1.crud 컨트롤러와 2.모델 3.라우트 4.컨트롤러에 액션)

```ruby
  private
    # Use callbacks to share common setup or constraints between actions.
    def set_post
      @post = Post.find(params[:id])
    end

    # Never trust parameters from the scary internet, only allow the white list through.
    def post_params
      params.require(:post).permit(:title, :content)
    end
```

## 액션이 시작되기전 !
+ before_action :set_post, only: [:show, :edit, :update, :destroy]
+ 위 네개의 액션(show,edit,update,destroy) 들은 특정 post 에 해당하는 액션을 수행하므로

## strong parameter
+ form_tag -> params = {title: 'title', content: 'content'}
+ form_for -> params = {post: {title: 'title',contnet: 'content'}}
```
내가 허락한 것만 불러온다!
def post_params
      params.require(:post).permit(:title, :content)
    end
```
+ params.require(:post)까지 하면 {title: 'title', content: 'content'} 불러옴
+ .permit으로 조건화

## <%= render 'form' %>

+ edit 과 new 에서 <%= render 'form' %> 으로 _from.html.erb를 불러온다.
+ 중요한것은 같은 폴더내여야함.
+ @post가 무엇이냐에 따라, 달라지므로 똑같은 _form을 렌더하더라도 다른 기능가능.