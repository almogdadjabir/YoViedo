# Overview


![GitHub](https://img.shields.io/badge/android-%23326ce5.svg?style=for-the-badge&logo=android&logoColor=white)
![GitHub](https://img.shields.io/badge/java-%23006d77.svg?style=for-the-badge&logo=java&logoColor=white)
![GitHub](https://img.shields.io/badge/sqlite-%23ff8fab.svg?style=for-the-badge&logo=sqlite&logoColor=white)
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)
![GitHub](https://img.shields.io/badge/kotlin-%23f72585.svg?style=for-the-badge&logo=kotlin&logoColor=white)
![GitHub](https://img.shields.io/badge/lottie-%23f7a072.svg?style=for-the-badge&logo=lottie&logoColor=white)
![GitHub](https://img.shields.io/badge/mvvm-%23e0fbfc.svg?style=for-the-badge&logo=mvvm&logoColor=black)
![GitHub](https://img.shields.io/badge/room-%23ee6c4d.svg?style=for-the-badge&logo=room&logoColor=white)
![GitHub](https://img.shields.io/badge/lifecycle-%23e7ecef.svg?style=for-the-badge&logo=lifecycle&logoColor=black)

## Oxinus Technical:

- ### This project is an assignment from the Oxinus Technical team.

## Demo


https://github.com/almogdadjabir/POS_Lenadorsystems/assets/49059742/31a81392-1fd4-45d2-9f23-8b26e93a6a5f



## Task Requirements

- A list of dog breeds<br/>
  As a user, you should be able to:
  > See dog breeds, 
  > Tap on a dog breed and go to that dog breed screen

- A dog breed screen<br/>
  As a user, you should be able to:

  > See multiple images of that specific dog breed, Tap on a button on a dog breed image to like/unlike it

- A favorite images screen<br/>
  As a user, you should be able to:
  > See liked dog breed images including what dog breed it belong to, Filter images by selecting a breed. 


<br>
<hr>
<be>

## Database Schema

#### Dog Table

| #     | title        | Type   | Note   |
| ----- | ------------ | ------ | ------ |
| 1     | id           | long   | PK     |
| 2     | image        | String |        |
| 3     | breed        | String |        |



<br>
<hr>
<be>

## Screens
- SplashScreen
    1. Activity with Lottie-file animation.
- MainActivity Screen
    1. List of breeds as Tabs.
         a. Dynamic Tab with Fragment.
    3. List of dogs filtrate by breeds </br>
       a. Add to Favorite. </br>
- Favorite Screen</br>
  a. Get All Dogs from that add to favorite from Database</br>
  b. Remove from Favourite (remove from UI and Database).

<br>
<hr>
<be>

## Architecture and Design Pattern:

I have employed the MVVM architecture, utilizing Room for data storage, DAO for database configuration, Repository for managing data at the data layer, and ViewModel to encapsulate UI-related logic and facilitate data transfer.

<br>
<hr>
<be>


<be>

- Add Dynamic Tab with his own Fragment.

```java
private void getBreeds() {
        dogBreedsViewModel.getDogBreedsLiveData().observe(this, dogsResponse -> {
            mShimmerViewContainer.stopShimmerAnimation();
            mShimmerViewContainer.setVisibility(View.GONE);
            if (dogsResponse != null) {


                List<String> breeds = dogsResponse.getMessage();

                saveListToSharedPreferences(breeds, "breeds");

                for (String breed : breeds) {
                    mTabLayout.addTab(mTabLayout.newTab().setText(breed));
                }

                BreedsFragmentAdapter mBreedsFragmentAdapter = new BreedsFragmentAdapter(getSupportFragmentManager());
                mBreedsFragmentAdapter.setDogBreeds(breeds);
                viewPager.setAdapter(mBreedsFragmentAdapter);
                viewPager.setCurrentItem(0);

            }
        });
    }
```

<br>
<hr>
<be>

