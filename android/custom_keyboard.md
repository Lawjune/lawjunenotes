## 1. Create a no-activity project

*Because this project doesn't need `Activity` to run, we will run `Service` so we will not create activity.*

## 2. Declare `color` for the keyboard

**Insert the following configurations into `/res/values/color.xml`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="purple_200">#FFBB86FC</color>
    <color name="purple_500">#FF6200EE</color>
    <color name="purple_700">#FF3700B3</color>
    <color name="teal_200">#FF03DAC5</color>
    <color name="teal_700">#FF018786</color>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>

    <!-- Colors for the keyboard -->
    <color name="keyboard_background_color">#34459e</color>
    <color name="keyboard_divider">#2c3e50</color>
    <color name="keyboard_pressed">#95a5a6</color>
</resources>
``` 

## 3. Create method.xml and declare lable, type of the keyboard

**Create new a new folder -> `/res/xml`**
**Create file -> `/res/xml/method.xml`**


*res/xml/method.xml*
```xml
<?xml version="1.0" encoding="utf-8"?>
<input-method xmlns:android="http://schemas.android.com/apk/res/android">
    <subtype
        android:label="English (US)"
        android:imeSubtypeLocale="en_US"
        android:imeSubtypeMode="keyboard"
        />
</input-method>
```

## 4. Create the keyboard UI - QWERTY keyboard

**Create file -> `/res/xml/qwerty.xml`**

*`/res/xml/qwerty.xml`*
```xml
<?xml version="1.0" encoding="utf-8"?>
<Keyboard xmlns:android="http://schemas.android.com/apk/res/android"
    android:keyWidth="10%p"
    android:horizontalGap="0px"
    android:verticalGap="0px"
    android:keyHeight="60dp">

    <Row>
        <Key android:keyLabel="1"
            android:keyEdgeFlags="left"
            android:codes="49" />
        <Key android:keyLabel="2"
            android:codes="50" />
        <Key android:keyLabel="3"
            android:codes="51" />
        <Key android:keyLabel="4"
            android:codes="52" />
        <Key android:keyLabel="5"
            android:codes="53" />
        <Key android:keyLabel="6"
            android:codes="54" />
        <Key android:keyLabel="7"
            android:codes="55" />
        <Key android:keyLabel="8"
            android:codes="56" />
        <Key android:keyLabel="9"
            android:codes="57" />
        <Key android:keyLabel="0"
            android:keyEdgeFlags="right"
            android:codes="48" />
    </Row>

    <Row>
        <Key android:codes="113" android:keyLabel="q" android:keyEdgeFlags="left"/>
        <Key android:codes="119" android:keyLabel="w"/>
        <Key android:codes="101" android:keyLabel="e"/>
        <Key android:codes="114" android:keyLabel="r"/>
        <Key android:codes="116" android:keyLabel="t"/>
        <Key android:codes="121" android:keyLabel="y"/>
        <Key android:codes="117" android:keyLabel="u"/>
        <Key android:codes="105" android:keyLabel="i"/>
        <Key android:codes="111" android:keyLabel="o"/>
        <Key android:codes="112" android:keyLabel="p" android:keyEdgeFlags="right"/>
    </Row>

    <Row>
        <Key android:codes="97" android:keyLabel="a" android:keyEdgeFlags="left"/>
        <Key android:codes="115" android:keyLabel="s"/>
        <Key android:codes="100" android:keyLabel="d"/>
        <Key android:codes="102" android:keyLabel="f"/>
        <Key android:codes="103" android:keyLabel="g"/>
        <Key android:codes="104" android:keyLabel="h"/>
        <Key android:codes="106" android:keyLabel="j"/>
        <Key android:codes="107" android:keyLabel="k"/>
        <Key android:codes="108" android:keyLabel="l"/>
        <Key android:codes="35, 64" android:keyLabel="\# \@" android:keyEdgeFlags="right"/>
    </Row>

    <Row>
        <Key android:codes="-1" android:keyLabel="CAPS" android:keyEdgeFlags="left"/>
        <Key android:codes="122" android:keyLabel="z"/>
        <Key android:codes="120" android:keyLabel="x"/>
        <Key android:codes="99" android:keyLabel="c"/>
        <Key android:codes="118" android:keyLabel="v"/>
        <Key android:codes="98" android:keyLabel="b"/>
        <Key android:codes="110" android:keyLabel="n"/>
        <Key android:codes="109" android:keyLabel="m"/>
        <Key android:codes="46" android:keyLabel="."/>
        <Key android:codes="63, 33, 58" android:keyLabel="\? ! :" android:keyEdgeFlags="right"/>
    </Row>

    <Row android:rowEdgeFlags="bottom">
        <Key android:codes="44" android:keyLabel="," android:keyEdgeFlags="left"
            android:keyWidth="10%p" />
        <Key android:codes="47" android:keyLabel="/"
            android:keyWidth="10%p" />
        <Key android:codes="32" android:keyLabel="SPACE" android:isRepeatable="true"
            android:keyWidth="40%p" />
        <Key android:codes="-5" android:keyLabel="DEL" android:isRepeatable="true"
            android:keyWidth="20%p" />
        <Key android:codes="-4" android:keyLabel="DONE" android:keyEdgeFlags="right"
            android:keyWidth="20%p" />
    </Row>


</Keyboard>
```

***Explain the code***
```xml
<Key android:keyLabel="1"           ->Label will display
    android:keyEdgeFlags="left"     -> Position of key
    android:codes="49" />           -> ASCII value "49" = 1
```

## 5. Create layout for this UI

*Right click on `/res` and "create a Andorid Resource Directory" named as `layout` -> `/res/layout`*

**Create a file -> `/res/layout/keyboard.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<android.inputmethodservice.KeyboardView
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/keyboard"
    android:layout_alignParentBottom="true"

    android:keyTextColor="@android:color/white"
    android:keyBackground="@drawable/key_background"
    android:keyPreviewLayout="@layout/key_preview"
    android:background="@color/design_default_color_primary_dark"

    android:layout_width="match_parent"
    android:layout_height="wrap_content">

</android.inputmethodservice.KeyboardView>
```

**Create a file -> `/res/layout/key_preview.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<TextView xmlns:android="http://schemas.android.com/apk/res/android"
    android:gravity="center"
    android:background="#5d5d5d"
    android:textColor="@android:color/white"
    android:textStyle="italic"
    android:textSize="30sp"

    android:layout_width="match_parent"
    android:layout_height="match_parent">

</TextView>
```

**Create a file -> `/res/drawable/key_background.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:state_focused="false"
        android:state_selected="false"
        android:state_pressed="false"
        android:drawable="@drawable/normal"
        />

    <item
        android:state_pressed="true"
        android:drawable="@drawable/pressed"
        />
</selector>
```

**Create a file -> `/res/drawable/normal.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:left="2dp" android:right="2dp">
        <shape android:shape="rectangle">
            <solid android:color="@color/keyboard_divider" />
        </shape>
    </item>

    <item android:bottom="2dp">
        <shape android:shape="rectangle">
            <solid android:color="@color/keyboard_background_color" />
        </shape>
    </item>
</layer-list>
```

**Create a file -> `/res/drawable/pressed.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="@color/keyboard_pressed" />
</shape>
```


***It needs to create new keyboard & key_preview layouts with new defined colors corresponding to the themes.***

## 6. Declare `Service` to run the keyboard

*Rigth click on `com.example.androidcustomkeyboard` to create a `Service` named as `EDMTKeyboard`.

```java
package com.example.androidcustomkeyboard;

import android.app.Service;
import android.content.Intent;
import android.inputmethodservice.InputMethodService;
import android.inputmethodservice.Keyboard;
import android.inputmethodservice.KeyboardView;
import android.media.AudioManager;
import android.os.IBinder;
import android.view.KeyEvent;
import android.view.View;
import android.view.inputmethod.InputConnection;

public class EDMTKeyboard extends InputMethodService implements KeyboardView.OnKeyboardActionListener {

    private KeyboardView kv;
    private Keyboard keyboard;

    private boolean isCaps = false;

    // Press Ctrl+O


    @Override
    public View onCreateInputView() {
        kv = (KeyboardView) getLayoutInflater().inflate(R.layout.keyboard, null);
        keyboard = new Keyboard(this, R.xml.qwerty);
        kv.setKeyboard(keyboard);
        kv.setOnKeyboardActionListener(this);
        return kv;
    }

    @Override
    public void onPress(int i) {

    }

    @Override
    public void onRelease(int i) {

    }

    @Override
    public void onKey(int i, int[] ints) {
        InputConnection ic = getCurrentInputConnection();
        playClick(i);
        switch (i) {
            case Keyboard.KEYCODE_DELETE:
                ic.deleteSurroundingText(1, 0);
                break;
            case Keyboard.KEYCODE_SHIFT:
                isCaps = !isCaps;
                keyboard.setShifted(isCaps);
                kv.invalidateAllKeys();
                break;
            case Keyboard.KEYCODE_DONE:
                ic.sendKeyEvent(new KeyEvent(KeyEvent.ACTION_DOWN, KeyEvent.KEYCODE_ENTER));
                break;
            default:
                char code = (char)i;
                if(Character.isLetter(code) && isCaps)
                    code = Character.toUpperCase(code);
                ic.commitText(String.valueOf(code), 1);
        }
    }

    private void playClick(int i) {
        AudioManager am = (AudioManager)getSystemService(AUDIO_SERVICE);
        switch (i) {
            case 32:
                am.playSoundEffect(AudioManager.FX_KEYPRESS_SPACEBAR);
                break;
            case Keyboard.KEYCODE_DONE:
            case 10:
                am.playSoundEffect(AudioManager.FX_KEYPRESS_RETURN);
                break;
            case Keyboard.KEYCODE_DELETE:
                am.playSoundEffect(AudioManager.FX_KEYPRESS_DELETE);
                break;
            default:
                am.playSoundEffect(AudioManager.FX_KEYPRESS_STANDARD);
        }
    }

    @Override
    public void onText(CharSequence charSequence) {

    }

    @Override
    public void swipeLeft() {

    }

    @Override
    public void swipeRight() {

    }

    @Override
    public void swipeDown() {

    }

    @Override
    public void swipeUp() {

    }
}
```

**Edit the `/manifest/AndroidManifest.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.androidcustomkeyboard">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.AndroidCustomKeyboard">
        <service
            android:name=".EDMTKeyboard"
            android:label="EDMTKeyboard"
            android:permission="android.permission.BIND_INPUT_METHOD"
            android:exported="false">
            <meta-data android:name="android.view.im" android:resource="@xml/method" />
            <intent-filter>
                <action android:name="android.view.InputMethod" />
            </intent-filter>
        </service>
    </application>

</manifest>
```

## 7 Set the `Build` type of Androdi Studio for "no launcher activity" app

<Run> -> <Edit Configuration> -> <Launch Options> -> Select as "Nothing" then build!

*Inject into your target and select it in "Input Method".*