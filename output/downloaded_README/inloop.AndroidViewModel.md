AndroidViewModel
================

<b>Important notice: Deprecated</b>
--------
<b>This library served it's purpose for over 3 years. We believe that Google's Android [Architecture Components](https://developer.android.com/topic/libraries/architecture/index.html) are the preferred setup now for new projects. </b>
<b>[INLOOPX](http://www.inloopx.com) is dedicated to continue maintaining this library (no deadline on support end). So rest assured that your existing projects don't need be migrated from AndroidViewModel because of this deprecation. We are only stopping new feature development and don't recommend using it for new projects.</b>


Separating data and state handling from Fragments or Activities without lots of boilerplate-code. Reducing them to simple <i>dumb views</i>.

<b>Basic idea behind this library</b>.
An instance of a ViewModel class is assigned to your Fragment or Activity during the first creation and is kept during it's life cycle, even between display orientation changes. The ViewModel instance is removed after the Fragment or Activity is completely gone (finished, popped from backstack, replaced without keeping it in backstack).

You can execute asynchronous tasks in this ViewModel instance and this class is not destroyed during orientation change. All data handling and state logic should be placed inside this class. The Fragment or Activity is just a "dumb" view.


How to implement
--------

1. Create an interface for your <b>View</b> by extending [IView](library/src/main/java/eu/inloop/viewmodel/IView.java). We will call it IUserListView for this example.

   ```java
    public interface IUserListView extends IView {
         public void showUsers(List<User> users);
    }

   ```
2. Create your <b>ViewModel</b> class by extending [AbstractViewModel](library/src/main/java/eu/inloop/viewmodel/AbstractViewModel.java). For example: <br/>

   ```java
   public class UserListViewModel extends AbstractViewModel<IUserListView> {
      ....
   }
   ```
3. Each <b>Fragment</b> or <b>Activity</b> that you would like to associate with a ViewModel will need either to extend [ViewModelActivityBase](library/src/main/java/eu/inloop/viewmodel/base/ViewModelBaseActivity.java)/[ViewModelBaseFragment](library/src/main/java/eu/inloop/viewmodel/base/ViewModelBaseFragment.java) or copy the implementation from these classes to your base activity/fragment class (in case you can't inherit directly). For example: <br/>
  
   ```java
   public class UserListFragment extends ViewModelBaseFragment<IUserListView, UserListViewModel> 
      implements IUserListView {
      
   }
   ```

4. Also each <b>Fragment</b> or <b>Activity</b> has to call ```setModelView()``` after the View (Fragment/Activity) was created and initialized. This is usually on the end of onViewCreated (or onCreate in case of an Activity) <br/>
  
   ```java
   @Override
   public void onViewCreated(View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        ButterKnife.inject(this, view);
        setModelView(this);
   }
   ```  
  
How to use
--------

You can forward user interaction from the View into the ViewModel simply by calling:

  ```java
  getViewModel().onDeleteUserClicked(userId);
  ```
  
The same goes for the opposite direction, when your asynchronous operation in the ViewModel finished and you would like to forward data to the View to show a list for example:

  ```java
  getViewOptional().showUsers(userList);
  ```

The ```getViewOptional()``` method will never return null. It will return a dummy implementation in case the View is null at the moment (e.g. Fragment already destroyed, or between orientation change).
You can also check if the View is not null in case you need to:  
  
  ```java
  if (getView() != null) {
      getView().showUsers(userList);
  }
  ```

Your Fragment argument Bundle and Activity intent Bundle is forwarded to the ViewModel's onCreate method, which you can override to read the initial arguments for the ViewModel.

   ```java 
   public void onCreate(Bundle arguments, Bundle savedInstanceState) {
      long userId = arguments.getInt("user_id", -1);
   }
   ``` 
    

Data binding support
--------
Data binding is supported - extend [ViewModelBaseBindingFragment.java](library/src/main/java/eu/inloop/viewmodel/binding/ViewModelBaseBindingFragment.java) instead of ViewModelBaseFragment and implement ```getViewModelBindingConfig()``` in your Fragment.

   ``` java
   @Override
   public ViewModelBindingConfig getViewModelBindingConfig() {
      return new ViewModelBindingConfig(R.layout.fragment_sample_binding, requireActivity());
   }
   ```

That's it. You can then directly use ObservableField in your ViewModels. See [example](sample/src/main/java/eu/inloop/viewmodel/sample/viewmodel/SampleBindingViewModel.java). 

Special handling for FragmentStatePagerAdapter
--------
The Android implementation of [FragmentStatePagerAdapter](https://developer.android.com/reference/android/support/v4/app/FragmentStatePagerAdapter.html) is removing Fragments and storing their state. This is in contrast with [FragmentPagerAdapter](https://developer.android.com/reference/android/support/v4/app/FragmentPagerAdapter.html) where the Fragments are just detached but not removed.
We should be also removing ViewModels and storing their state to be consistent with this behaviour.

<b>Use [ViewModelStatePagerAdapter](library/src/main/java/eu/inloop/viewmodel/support/ViewModelStatePagerAdapter.java) instead of the default FragmentStatePagerAdapter</b>. This class is only overriding the ```destroyItem()``` method and making sure that ViewModel is removed. The state is stored/restored automatically.
You can also use the standard FragmentStatePagerAdapter - in that case ViewModels will be kept in memory and removed only when you leave the screen (Activity finished or Fragment removed).

How does it work?
--------

A unique global ID is generated for the first time your Fragment or Activity is shown. This ID is passed on during orientation changes. Opening another instance of the same Fragment or Activity will result in a different ID. The ID is unique screen identifier. A ViewModel class is created and bound to this ID. The corresponding ViewModel instance is attached to your Fragment or Activity after an orientation change or if you return to the fragment in the back stack.
The ViewModel is discarded once the Fragment/Activity is not reachable anymore (activity is finished or fragment permanently removed).


Download
--------

```groovy
compile 'eu.inloop:androidviewmodel:1.3.5'
```

## Android Studio Template
For faster creating new screens, you can use [Android Studio Template](/template/AVM_Inloop)

![Android Studio Template Window](/template/template-preview.png)

### Install template
#### Manually:
Copy the template folder to Android Studio templates folder (`/Applications/Android Studio.app/Contents/plugins/android/lib/templates/others` on Mac)
#### Automatically:
Run the following command to download and install the template automatically (Mac only)
```
curl -o androidviewmodel.zip -Lk https://github.com/inloop/AndroidViewModel/archive/master.zip && unzip androidviewmodel.zip && cp -af AndroidViewModel-master/template/AVM_Inloop/. "/Applications/Android Studio.app/Contents/plugins/android/lib/templates/other/AVM_Inloop" && rm -r AndroidViewModel-master && rm androidviewmodel.zip
```
<b>Don't forget to restart the Android Studio.</b>

### Usage
In the Android Studio right click inside the Projet window and select `File > New > AndroidViewModel Inloop > AVM Fragment`


![Android Studio New Template](/template/create-new-template-preview.png)