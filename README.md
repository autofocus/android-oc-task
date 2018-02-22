## On-site assignment - Giphy App

The assignment is to build an app that allows users to browse the trending gifs using Giphy API, searching gifs, and saving those they like. Your job is to finish the app by implementing some of the key features listed below.

## Todo

1. Finish the `LoginActivity` to persist the login state between app launches such that next time the user will skip the activity if it's already logged in.
2. Add pagination support in `TrendingFragment` to make it loads the next page of gifs once the recycler view scrolls to the bottom.
3. Complete the searching functionality in `MainActivity` and `TrendingFragment` such that the search results will be displayed instead of the trending data when the query text is not empty. When query text is deleted, restore the previous trending data.
4. Complete the `GifPreviewActivity` by passing the selected gif from previous activity and display the original image in the image view. Prompt user to share the gif to other apps when the share button is tapped.
5. Introduce a persistent layer that saves Gif object marked as favorite. The favorite button in `GifPreviewActivity` will toggle the favorite state of the gif.
6. Show all favorite gifs in the **Favorite** tab in `FavoriteFragment` by using `RecyclerView`.

### Notes

* No limitation on other libraries

## GIPHY Android SDK

The SDK is integrated within the project. There are some basic usage required for the assignment:

```java
GPHApi client = new GPHApiClient("YOUR_API_KEY");
```

### Search Endpoint
Search all Giphy GIFs for a word or phrase. Punctuation will be stripped and ignored.

```java
/// Gif Search
client.search("cats", MediaType.gif, null, null, null, null, new CompletionHandler<ListMediaResponse>() {
    @Override
    public void onComplete(ListMediaResponse result, Throwable e) {
        if (result == null) {
            // Do what you want to do with the error
        } else {
            if (result.getData() != null) {
                for (Media gif : result.getData()) {
                    Log.v("giphy", gif.getId());
                }
            } else {
                Log.e("giphy error", "No results found");
            }
        }
    }
});
```

### Trending Endpoint
Fetch GIFs currently trending online. Hand curated by the Giphy editorial team. The data returned mirrors the GIFs showcased on the [Giphy](https://www.giphy.com) homepage.

```java
/// Trending Gifs
client.trending(MediaType.gif, null, null, null, new CompletionHandler<ListMediaResponse>() {
    @Override
    public void onComplete(ListMediaResponse result, Throwable e) {
        if (result == null) {
            // Do what you want to do with the error
        } else {
            if (result.getData() != null) {
                for (Media gif : result.getData()) {
                    Log.v("giphy", gif.getId());
                }
            } else {
                Log.e("giphy error", "No results found");
            }
        }
    }
});

/// Trending Stickers
client.trending(MediaType.sticker, null, null, null, new CompletionHandler<ListMediaResponse>() {
    @Override
    public void onComplete(ListMediaResponse result, Throwable e) {
        if (result == null) {
            // Do what you want to do with the error
        } else {
            if (result.getData() != null) {
                for (Media gif : result.getData()) {
                    Log.v("giphy", gif.getId());
                }
            } else {
                Log.e("giphy error", "No results found");
            }
        }
    }
});
```

## Reference
1. [GIPHY Developers](https://developers.giphy.com/docs/)
2. [GIPHY Android SDK](https://github.com/Giphy/giphy-android-sdk-core)