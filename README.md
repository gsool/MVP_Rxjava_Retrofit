# MVP_Rxjava_Retrofit

MVP+Retrofit+RxJava实战小Demo，可快速移植到自己的项目中进行运用。

本Demo主要涉及到以下内容：

1、如何将Retrofit+RxJava联网框架，结合泛型MVP架构，优雅灵活地运用到项目中。<br>
2、BaseMvpActivity和BaseMvpFragment的封装<br>
3、统一封装接口返回的json数据 <br>
4、自定义接口对网络请求的异常回调进行统一的处理。<br>
5、MVC、MVP架构的运用<br>


使用MVP+Retrofit+RxJava框架后Activity的代码：

```
/**
 * 测试MVP + Retrofit +RxJava
 */
public class MainActivity extends BaseMvpActivity<MainPresenter, MainModel> implements MainContract.View {
    @BindView(R.id.tv_quality)
    TextView tv_quality;
    @BindView(R.id.tv_pm)
    TextView tv_pm;
    @BindView(R.id.tv_wendu)
    TextView tv_wendu;
    @BindView(R.id.tv_notice)
    TextView tv_notice;

    @Override
    protected int getContentViewLayoutID() {
        return R.layout.activity_main;
    }

    @Override
    protected void initViewAndEvents() {
        //发起请求
        mMvpPresenter.getWeather("101030100", mMultipleStateView);
    }

    /**
     * 接口请求成功的回调方法
     *
     * @param bean
     */
    @Override
    public void getWeather(WeatherEntity bean) {
        Log.e("TAG", "请求成功");
        tv_quality.setText("空气质量：" + bean.quality);
        tv_pm.setText("Pm10" + bean.pm10);
        tv_wendu.setText("温度：" + bean.wendu);
        tv_notice.setText("提醒：" + bean.ganmao);
    }
}

```

详情讲解可阅读文章[高级MVP+Retrofit+RxJava实战——一步步带你搭建一套好用的项目框架](https://www.jianshu.com/p/02030cdca283)
