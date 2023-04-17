# Google API from time to time changes the keys in the profile map it provides

The times we have noticed this and checked in a fix:

- April 17, 2023 [commit](https://github.com/Picolab/Manifold/commit/844dd1ed8c950de69a298012983999d20a3927e8)
- August 6, 2022 [commit](https://github.com/Picolab/Manifold/commit/7cbf9c053a299b93eac871a6ef0ee37a37e3a6fc)
- April 28, 2022 [commit](https://github.com/Picolab/Manifold/commit/f04aa21eae7fcb7dc2447050bc8ace332c29b91b)
- September 14, 2021 [commit](https://github.com/Picolab/Manifold/commit/f95cc4e754f746f1c5842fd434ea3e300d957d8b)
- March 5, 2021 [commit](https://github.com/Picolab/Manifold/commit/35de956b1ef5f22ea54f383ab6115ae81bd9f4bb#diff-ee0d263c8b39fae22976099a1baff0e19527479cf9892cd40cda9916e70b6b1a)
- August 3, 2020 [commit](https://github.com/Picolab/Manifold/commit/800ef7220c8244b8844143acfdee1bfed8dbc9df#diff-ee0d263c8b39fae22976099a1baff0e19527479cf9892cd40cda9916e70b6b1a)
- March 3, 2020 [commit](https://github.com/Picolab/Manifold/commit/4368590803c1acabe482631de40f7ce9e6cf70ed#diff-ee0d263c8b39fae22976099a1baff0e19527479cf9892cd40cda9916e70b6b1a)
- and they hadn't changed before that since originally written August 16, 2019 [commit](https://github.com/Picolab/Manifold/commit/a55803672d491a66bce4478082c7cbe6b1236436#diff-ee0d263c8b39fae22976099a1baff0e19527479cf9892cd40cda9916e70b6b1a)

No idea why Google would do this, but there is a bit of a pattern perhaps, at least lately, of early August and March.

The symptom is that the avatar and name appearing in the upper right corner after logging in with Google are missing. 
Instead there is a broken image and the word "Avatar".

## How to fix the problem

1. Find the file in the Manifold repo [Manifold_krl/io.picolabs.profile.krl](https://github.com/Picolab/Manifold/blob/master/Manifold_krl/io.picolabs.profile.krl)
2. Add a `klog` to [line 82](https://github.com/Picolab/Manifold/blob/master/Manifold_krl/io.picolabs.profile.krl#L82) so that you'll be able to see what Google provides
3. Logout and back in to Manifold; check your owner pico's Logging tab, looking for `event/ECI/EID/profile/google_profile_save`
4. Modify the code to use the new keys
5. Push your changes
6. Wait a bit to be sure the raw version of the ruleset on GitHub has the changes
7. Flush the ruleset (or reinstall from the raw URL)
8. Log out and back in to Manifold to see your avatar and name

Make a note to check again in 5-7 months.

## Code before the latest change

[_in situ_](https://github.com/Picolab/Manifold/blob/54fa42dbb63f6d87e085d027c1cef9d2ddeb65d4/Manifold_krl/io.picolabs.profile.krl#L79-L103)
```
      profile = event:attr("profile") // .klog("profile") // here in line 82
      googleProfile = {
        "displayName" : profile["ig"] || profile{"Cd"},
        "firstName" : profile["ofa"] || profile{"sW"},
        "lastName" : profile["wea"] || profile{"sU"},
        "profileImgURL" : profile["Paa"] || profile{"PK"},
        "email" : profile["U3"] || profile{"yu"}
```

## The information from Google in logs

```
{
  "kR": "104366082891378509653",
  "sd": "Pico Labs",
  "QS": "Pico",
  "SQ": "Labs",
  "jI": "https://lh3.googleusercontent.com/a-/AOh14Gi7Q2PNj6X0O6crW39JnsdvKwwDqsG9Yilw7p-1=s96-c",
  "nt": "picolabsbyu@gmail.com"
}
```

Notice that there are two places in the code where the "email" key is mentioned. TODO fix that

