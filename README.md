# django-echarts

![django-echarts version](https://img.shields.io/pypi/v/django-echarts.svg) ![python27](https://img.shields.io/badge/Python-2.7+-blue.svg) ![python35](https://img.shields.io/badge/Python-3.5+-blue.svg) ![django18](https://img.shields.io/badge/Django-1.8+-blue.svg)

A intergration for [Echarts](http://echarts.baidu.com/index.html) and [Django](https://www.djangoproject.com) based on [chenjiandongx/pyecharts](https://github.com/chenjiandongx/pyecharts) .

> This project is on the developement state, do not use in the production environment.


## Requirements

- Python2.7+ / Python3.5+
- Django 1.8+
- echarts 3.1+

## Basic Uage

views.py

```python
from django.views.generic.base import TemplateView
from pyecharts import Bar
from django_echarts import EchartsView

class IndexView(TemplateView):
    template_name = 'index.html'

class SimpleBarView(EchartsView):
    def get_echarts_option(self, **kwargs):
        bar = Bar("我的第一个图表", "这里是副标题")
        bar.add("服装", ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"], [5, 20, 36, 10, 75, 90])
        return bar._option
```

urls.py

```python
from django.conf.urls import url

from .views import IndexView, SimpleBarView

urlpatterns = [
    url(r'^$', IndexView.as_view()),
    url(r'options/simpleBar/', SimpleBarView.as_view())
]
```

html

```html
<div id="id_echarts_container" style="height: 500px;"></div>

<script type="text/javascript">
    $(document).ready(function () {
        var mChart = echarts.init(document.getElementById('id_echarts_container'));
        $.ajax({
            url: '/options/simpleBar/',
            type: "GET",
            dataType: "json"
        }).done(function (data) {
            mChart.setOption(data);
        });
    });
</script>
```

## API

(No document)

## Example

The example project is under *example* directory.

```shell
cd example
python manage.py runserver 127.0.0.1:8000
```

Access the web url  http://127.0.0.1:8000 , the screencut is the following picture.

![Demo](images/demo1.gif)

## License

The project is under the MIT license, Issues & Pull requests are welcome.