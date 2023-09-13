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

We are using Room as an Object-Relational Mapping (ORM) tool to manage our SQLite database. Currently, we have only one table that handles the favorite feature, and here is the schema for the "Dog" table:

#### Dog Table

| #     | title        | Type   | Note   |
| ----- | ------------ | ------ | ------ |
| 1     | id           | long   | PK     |
| 2     | image        | String |        |
| 3     | breed        | String |        |

<br>
This "Dog" table serves as the foundation for managing our favorite feature within the database.
<br><br>

```java
@Dao
public interface DogDao {

    @Insert(onConflict = OnConflictStrategy.IGNORE)
    void insert(Dog dog);

    @Update
    void update(Dog product);

    @Delete
    void delete(Dog product);

    @Query("Delete FROM dog_table")
    void deleteAllDogs();

    @Query("SELECT * FROM dog_table")
    LiveData<List<Dog>> getAllDogs();

    @Query("SELECT * FROM dog_table WHERE breed = :breeds")
    LiveData<List<Dog>> getDogByBreeds(String breeds);
}
```

<br>
<hr>
<be>

## Screens
- SplashScreen
    1. An activity featuring a Lottie-file animation.
- MainActivity Screen
    1. A screen displaying a list of breeds as tabs.</br>
         a. Each tab is dynamic and corresponds to a fragment.</br>
    3. A list of dogs filtered by breeds </br>
       a.Ability to add dogs to favorites. </br>
- Favorite Screen</br>
    1. Displays all dogs that have been added to the favorites.</br>
    2. Provides an option to remove dogs from favorites, both from the UI and the database.
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

