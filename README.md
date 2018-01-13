# vueZoom
vue放大镜组件
## 使用
    import vueZoom from 'vueZoom'
    <template>
        <vue-zoom sImg='smallImgSrc' 
        bImg='bigImgSrc' 
        :sSize="{width:300,height:200}" 
        :bSize='{width:500,height:500}' 
        :mSize={width:100,height:100}></vue-zoom>
    </template>
## 参数说明:
 - sImg 放大镜中小图的图片地址
 - bImg 放大镜中大图的图片地址(src可以与小图相同)
 - sSize 放大镜中小图显示的大小
 - bSize 放大镜大图显示的可见部分的大小
 - mSize 放大镜小图上的可移动蒙版大小 
## Ps:
可移动蒙版样式未使用自定义,可直接修改源码样式
