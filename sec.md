# Overview


![GitHub](https://img.shields.io/badge/flutter-%23326ce5.svg?style=for-the-badge&logo=flutter&logoColor=white)
![GitHub](https://img.shields.io/badge/ios-%237400b8.svg?style=for-the-badge&logo=ios&logoColor=white)
![GitHub](https://img.shields.io/badge/android-%2380ed99.svg?style=for-the-badge&logo=android&logoColor=white)
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)
![GitHub](https://img.shields.io/badge/swift-%23f25c54.svg?style=for-the-badge&logo=swift&logoColor=white)
![GitHub](https://img.shields.io/badge/kotlin-%23f72585.svg?style=for-the-badge&logo=kotlin&logoColor=white)
![GitHub](https://img.shields.io/badge/mvvm-%23e0fbfc.svg?style=for-the-badge&logo=mvvm&logoColor=black)
![GitHub](https://img.shields.io/badge/getx-%23735751.svg?style=for-the-badge&logo=getx&logoColor=white)
![GitHub](https://img.shields.io/badge/get-storage-%23ffd100.svg?style=for-the-badge&logo=getstorage&logoColor=white)
![GitHub](https://img.shields.io/badge/get-it-%238c1c13.svg?style=for-the-badge&logo=getit&logoColor=white)
![GitHub](https://img.shields.io/badge/lottie-%23967aa1.svg?style=for-the-badge&logo=lottie&logoColor=white)


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

## Screens
- Main Screen
    1. A screen displaying a list of breeds</br>
    2. A list of dogs filtered by breeds </br>
       a.Ability to add dogs to favorites. </br>
- Favorite Screen</br>
    1. Displays all dogs that have been added to the favorites.</br>
    2. Provides an option to remove dogs from favorites, both from the UI and the local-storage.
<br>
<hr>
<be>

## Architecture and Design Pattern:

I have employed the MVVM architecture, utilizing Room for data storage, DAO for database configuration, Repository for managing data at the data layer, and ViewModel to encapsulate UI-related logic and facilitate data transfer.

<br>
<hr>
<be>


<be>

- Get random image

```dart
static Future<RandomImage?> randomImage() async {

    String endpointUrl = "${Constants.baseUrl}api/breeds/image/random";
    RandomImage data;
    try {

      Response response = await getIt<Dio>().get(endpointUrl,);

      if (response.statusCode == 200) {
        data = RandomImage.fromJson(response.data);
        return data;

      } else {
        return null;
      }
    } catch (e) {
      return null;
    }
  }
```

call the function </br>

```dart
void getRandomImage() async {
    changeLoading(true);

    RandomImage? response = await HomeAPIRequest.randomImage();

    if(response != null){
      randomImage = response.message!;
      changeLoading(false);
    }else{
      changeLoading(false);
    }

  }
```

<br>
<hr>
<be>

