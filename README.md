Android-Lib-reCAPTCHA
=====================

[![Download](https://api.bintray.com/packages/ayltai/maven/Android-Lib-reCAPTCHA/images/download.svg)](https://bintray.com/ayltai/maven/Android-Lib-reCAPTCHA/_latestVersion) [![Build Status](https://travis-ci.org/ayltai/Android-Lib-reCAPTCHA.svg?branch=master)](https://travis-ci.org/ayltai/Android-Lib-reCAPTCHA) [![CircleCI](https://circleci.com/gh/ayltai/Android-Lib-reCAPTCHA/tree/master.svg?style=svg)](https://circleci.com/gh/ayltai/Android-Lib-reCAPTCHA/tree/master) [![Codeship Status for ayltai/Android-Lib-reCAPTCHA](https://codeship.com/projects/11617a20-0542-0134-c052-52d3a6e8b2fb/status?branch=master)](https://codeship.com/projects/154375) [![Build Status](https://www.bitrise.io/app/f841e281ea9f60f8.svg?token=vz-fpO2sL5otS0IGQegCSA&branch=master)](https://www.bitrise.io/app/f841e281ea9f60f8)  [![BuddyBuild](https://dashboard.buddybuild.com/api/statusImage?appID=5748647cff80170100275e94&branch=master&build=latest)](https://dashboard.buddybuild.com/apps/5748647cff80170100275e94/build/latest)

The reCAPTCHA Android Library provides a simple way to show a <a href="http://www.google.com/recaptcha/captcha">CAPTCHA</a> as an <code>ImageView</code> in your Android app, helping you stop bots from abusing it. The library wraps the <a href="https://developers.google.com/recaptcha/intro">reCAPTCHA API</a>.

<img src="https://raw.githubusercontent.com/ayltai/Android-Lib-reCAPTCHA/master/screenshot.png" width="422" height="714" alt="Screenshot" />

Quick Start
-----------

First you have to <a href="https://www.google.com/recaptcha/admin">sign up for your API keys</a>.

**Installation**

<pre>
repositories {
    jcenter()
}

dependencies {
    compile 'android.lib.recaptcha:reCAPTCHA:+'
}
</pre>

**The Layout**

To show CAPTCHA image, you need to add a `<android.lib.recaptcha.ReCaptcha />` element to your layout XML:

<pre>
&lt;android.lib.recaptcha.ReCaptcha
    android:id="@+id/recaptcha"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:scaleType="centerInside" /&gt;
</pre>

It is important to use `android:scaleType="centerInside"` to ensure the entire <a href="http://www.google.com/recaptcha/captcha">CAPTCHA</a> image can be displayed.

Alternatively, you can create an instance of `android.lib.recaptcha.ReCaptcha` at runtime:

<pre>ReCaptcha reCaptcha = new ReCaptcha(context);</pre>

**How to show CAPTCHA**

In your activity/fragment/view containing `android.lib.recaptcha.ReCaptcha`, you need display a <a href="http://www.google.com/recaptcha/captcha">CAPTCHA</a> image for the user to response:

<pre>
ReCaptcha reCaptcha = (ReCaptcha)findViewById(R.id.recaptcha);
reCaptcha.showChallengeAsync("your-public-key", onShowChallengeListener);
</pre>

`showChallengeAsync` downloads and shows <a href="http://www.google.com/recaptcha/captcha">CAPTCHA</a> image asynchronously. It is safe to invoke in UI thread. No exception will be thrown in case of any error by this call. All errors will be treated as unsuccessful in showing <a href="http://www.google.com/recaptcha/captcha">CAPTCHA</a> image.

`onShowChallengeListener` is an instance of `ReCaptcha.OnShowChallengeListener`, which is called when an attempt to show a <a href="http://www.google.com/recaptcha/captcha">CAPTCHA</a> is completed.

The synchronous version of this method is `showChallenge`.

**How to verify user input**

To verify user input, pass the input string to `ReCaptcha.verifyAnswerAsync` (or `ReCaptcha.verifyAnswer`):

<pre>reCaptcha.verifyAnswerAsync("your-private-key", "user-input", onVerifyAnswerListener);</pre>

`verifyAnswerAsync` asynchronously submits the user input string to reCAPTCHA server for verification. It is safe to invoke in UI thread. No exception will be thrown in case of any error by this call. All errors will be treated as verification failure.

`onVerifyAnswerListener` is an instance of `ReCaptcha.OnVerifyAnswerListener`, which is called when an attempt to verify the user input is completed.

The synchronous version of this method is `verifyAnwser`.

**Specify a locale**

You can force the widget to render in a specific language. Please refer to [this page](https://developers.google.com/recaptcha/docs/language).

`reCaptcha.setLanguageCode("fr");`

Sample Application
------------------

A complete sample application is available at <a href="https://github.com/ayltai/Android-Lib-reCAPTCHA/tree/master/reCAPTCHA-Samples">https://github.com/ayltai/Android-Lib-reCAPTCHA/tree/master/reCAPTCHA-Samples</a>.
