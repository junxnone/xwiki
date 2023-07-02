-----

| Title         | Tools Jupyter ShowImageDynamic                      |
| ------------- | --------------------------------------------------- |
| Created @     | `2020-11-01T07:58:42Z`                              |
| Last Modify @ | `2022-12-22T06:19:02Z`                              |
| Labels        | \`\`                                                |
| Edit @        | [here](https://github.com/junxnone/xwiki/issues/72) |

-----

# 动态显示图片

## Reference

  - [如何在jupyter
    notebook中播放视频（不停地展示图片）](https://blog.csdn.net/BlowfishKing/article/details/81502432)

## 使用 ipython.display.display

    from IPython.display import clear_output, Image, display
    import base64
    import time
    
    def show_img(image):
        clear_output(wait=True)
        ret, png = cv2.imencode('.png', image)
        time.sleep(0.02)
        display(Image(data=png))
