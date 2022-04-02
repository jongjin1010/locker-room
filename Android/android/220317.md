# SingleLiveEvent , Event

오늘은 강의에서 제대로 짚고가지 못한 SingleLiveEvent 와 Event 에 대해 알아보려고 한다

<br>

> **😎 SingleLiveEvent 란 무엇일까**
---
**viewmodel** 을 사용하다 보면 이벤트가 발생을 했어도 굳이 어떠한 값을 넘겨주지 않아도 될 때가 있다

이럴때는 원래 **null**값을 넣어주거나 **불필요한** 값을 넣어주는 방법을 사용했다

하지만 이 방법은 그닥 좋지 않았고 이에 대한 해답으로 구글에서 **SingleLiveEvent** 라는 예시를 제공했다

<br>

>**🤔 왜 SingleLiveEvent 를 사용해야할까**
---

**ViewModel** 에서 **startMyActivity()** 란 메소드 호출이 발생하면 **View** 에서 감지하고 있다가 

**MyActivity** 를 실행해야한다고 가정했을때 **LiveData**를 이용해서 구현을 하는 상황에서

**SingleLiveEvent** 의 유무를 비교해보자

<br>

>> 기존

*viewmodel*
```kotlin
class MyViewModel : BaseViewModel() {

    val eventMyActivity: MutableLiveData<Boolean> = MutableLiveData() 


    fun startMyActivity() {
        eventMyActivity.value = true
    }
    
}
```
*activity*
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val viewModel = MyViewModel()

        viewModel.eventMyActivity.observe(this, {
            Intent(this, MyActivity::class.java).apply { 
                startActivity(this)
            }
        })

    }
}

```

위의 코드는 **SingleLiveEvent** 가 없는 기존의 방식이다

이 코드의 문제는 LiveData에 사용하지도 않는 불필요 값을 넣어야 한다

<br>

>> SingleLiveEvent
---

이제는 **SingleLiveEvent** 를 활용하여 위의 문제를 보완해보자

*SingleLiveEvent*
```kotlin
class SingleLiveEvent<T> : MutableLiveData<T>() {

    companion object {
        private const val TAG = "SingleLiveEvent"
    }

    val mPending: AtomicBoolean = AtomicBoolean(false)

    override fun observe(owner: LifecycleOwner, observer: Observer<in T>) {
        if (hasActiveObservers()) {
            Log.w(TAG,"Multiple observers registered but only one will be notified of changes.")
        }

        // Observe the internal MutableLiveData
        super.observe(owner, Observer { t ->
            if (mPending.compareAndSet(true, false)) {
                observer.onChanged(t)
            }
        })
    }

    @MainThread
    override fun setValue(@Nullable t: T?) {
        mPending.set(true)
        super.setValue(t)
    }

    /**
     * Used for cases where T is Void, to make calls cleaner.
     */
    @MainThread
    fun call() {
        value = null
    }

}
```

*viewmodel*

```kotlin
class MyViewModel : BaseViewModel() {

    private val _eventMyActivity = SingleLiveEvent<Any>()
    val eventMyActivity: LiveData<Any>
        get() = _eventMyActivity
            
            
    fun startMyActivity() {
        _eventMyActivity.call()
    }

}
```

*activity*
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val viewModel = MyViewModel()

        viewModel.eventMyActivity.observe(this, {
            Intent(this, MyActivity::class.java).apply { 
                startActivity(this)
            }
        })

    }
}
```

이런식으로 사용하면 불필요한 값을 넘겨주지 않고 call() 이란 메소드를 호출하는 것만으로도 

View에서 감지하여 이벤트를 실행할 수 있다

하지만 여기서 또 모든 이벤트마다 매번 SingleLiveData 객체를 만들어줘야 하는 문제가 발생한다

이때는 Event.kt 를 사용하여야 한다

<br>

>> Event
---

```kotlin
/**
 * Used as a wrapper for data that is exposed via a LiveData that represents an event.
 */
open class Event<out T>(private val content: T) {

    var hasBeenHandled = false
        private set // Allow external read but not write

    /**
     * Returns the content and prevents its use again.
     */
    fun getContentIfNotHandled(): T? {
        return if (hasBeenHandled) {
            null
        } else {
            hasBeenHandled = true
            content
        }
    }

    /**
     * Returns the content, even if it's already been handled.
     */
    fun peekContent(): T = content
}
```

여기서 만든 Event를 BaseViewModel 이라는 모든 ViewModel이 상속받는 

SuperClass에 다음과 같이 넣어 주었다

*baseviewmodel*
```kotlin
open class BaseViewModel : ViewModel() {

    private val _viewEvent = MutableLiveData<Event<Any>>()
    val viewEvent: LiveData<Event<Any>>
        get() = _viewEvent

    fun viewEvent(content: Any) {
        _viewEvent.value = Event(content)
    }

}
```

이렇게 한 뒤 viewmodel 에서 다음과 같이 사용할 수 있다

*viewmodel*
```kotlin
class MyViewModel : BaseViewModel() {

    companion object {
        const val EVENT_START_MY_ACTIVITY = 22212
    }

    fun startMyActivity() = viewEvent(EVENT_START_MY_ACTIVITY)

}
```

그리고 view 에서도 다음과 같이 사용한다

*activity*
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val viewModel = MyViewModel()

        viewModel.viewEvent.observe(this, {
            it.getContentIfNotHandled()?.let { event -> 
                when (event) {
                    MyViewModel.EVENT_START_MY_ACTIVITY -> {
                        Intent(this, MyActivity::class.java).apply {
                            startActivity(this)
                        }
                    }
                }
            }
        })

    }
}
```

이렇게 하게 되면 매번 SingleLiveEvent를 만들 필요도 없고

 여러 이벤트에 대해서 한번에 처리할 수도 있다







 