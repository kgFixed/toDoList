# At the end of the first part

1. What I've done

## fix_ror.org

In this repository, I retrieve a dump of the ror database in json. I created the python file to transform the json into rdf file for each organisation. But, the dump is just one json with all the data inside, about all the organisations. It's the reason why I made two scripts to have a rdf file with all the organisations in the same file, and one script which create a file for each rdf organisation.

This part of the project works, but I will have to do the new detection of release to know when I have to retrieve a new dump with the data. However, it's not the best method to do that. In fact, I already retrieve all the data for each release, so I can push the data of the latest release inside my folder to have the new rdf file.

### Details:

- scripts/all_grouped_organisation.py   -> transform json dump to rdf (1 file)
- scripts/all_separate_organisation.py  -> transform each organisation into rdf (Number_organisation files)

## store_ror.org

In this directory, I was able to make a clone of the ror.org directory, containing all the records for all the releases. The format of this data is json. The best thing to do for the future would be to avoid mixing release data directly into the same repository as scripts and other data. The same goes for retrieving schemas that I copy instead of testing them from a remote git repo.

As for what I was able to do with this data. I started by making a clone of the directory as I said, and then transforming it into rdf format. To do this, I had to go through a number of steps, which I'll detail here.

I started by going through all my repositories so that I could "study" each json or each release. To do this, I used the release_rdf_push function, which centralises the use of all the other functions. Then I go into process_ror_file, in order to detect the version of the json schema and then associate the correct template. In fact, before using subyt, it's essential to create a template corresponding to the json schema. In some particular cases, no version is detected, so each template must be tested on the json in order to associate it with the correct one. The "wrong" templates will return an error. Then, once the right template has been associated, I'll use the json_to_individual_rdf function to launch the conversion between json and rdf. Once the conversion is complete for each json in the release, there is a certain amount of time before the code moves on to the next one. This is because, in order to have a history of each release on github, we need to do a commit & push on the server. To do this, I've added the git_push_existing_ttl function, which automates commits & pushes to github between two releases. This creates a tag on github for each release. In the details of this tag, we can find the files of the associated organisations and the associated modifications.

### Details:

- scripts/create_rdf_file.py   ->  transform json file in rdf file
- scripts/detect_version.py    ->  detects the version of the ror json schema
- scripts/git_commitpush.py    ->  commit and push to github between releases
- scripts/release_rdf_push.py  ->  central file, go through the releases ror
- scripts/template_to_try.py   ->  associates the template with the version of the ror schema




2. What I still have to do