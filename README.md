# Welcome to Balder photo gallery

Made by Espen Antonsen.

Version 1.3.0 for Rails 3.2. See the rails2 branch for previous version.

http://balderapp.com

## Features

* Stores photos to disk in folders or on S3 (can run from Heroku...yay)
* Create multiple thumbnails of custom sizes
* Read and writes EXIF/IPTC title, description and keywords
* Organize in albums (as events in iPhoto)
* Combine albums in collections (as albums in iPhoto)
* Upload multiple photos
* Tag photos. Can also tag albums (actually all photos in album is tagged)
* User management with roles and permissions
* Geo-location of albums & photos with Google Maps integration.
* Authenticate with Facebook Connect

## Optional image processing

Default Balder uses mini_magick and mini_exiftool_vendored.

Optional:

- ImageMagicK. Carrierwave can use either RMagicK or MiniMagicK (default). To change resize option the correct gem must be used (specified in Gemfile) and change included setting for Carrierwave in file_uploader.rb
Can be installed from: http://www.imagemagick.org
- ImageScience which requires FreeImage. Can be installed from: http://sourceforge.net/projects/freeimage/
- ExifTool (required for Mini_EfixTool). Can be disabled. Default is to read EXIF tags but not write them to the file when database is updated as writing EXIF is slow. To enable just uncomment exif_write in photo.rb
Can be installed from: http://www.sno.phy.queensu.ca/~phil/exiftool/


## Configuration

config/balder.rb has the following adjustable settings:

* **STORAGE_PATH** Relative path to where the photos are stored. Default: uploads. Under the specified path two folders are used. "files" for original files and "thumbs" for generated thumbnails. This can be adjusted in app/uploaders/file_uploader.rb
* **PRIVATE** Require visitors to have a user and authenticate before viewing photos.
* **TITLE** Title of site
* **HEROKU** To be used on heroku.com. This will adjust carrierwave to save to Heroku's tmp area.
* **S3_KEY** For saving files to Amazon S3 (required for Heroku)
* **S3_SECRET** For saving files to Amazon S3 (required for Heroku)
* **S3_BUCKET** For saving files to Amazon S3 (required for Heroku)
* **FACEBOOK_ID** The id for your Facebook application for Facebook Connect authentication
* **FACEBOOK_SECRET** The secret for your Facebook application for Facebook Connect authentication

As these are environment variables [you can easily add them to Heroku](http://devcenter.heroku.com/articles/config-vars#rack_env_rails_env_merb_env). For a brief introduction to how to set up Balder on Heroku see [this blog post](http://blog.inspired.no/rails-photo-gallery-balder-on-heroku-and-s3-726).

## Installation

1. Clone the project from GitHub or Gitorious:
	GitHub: git clone git://github.com/espen/balder.git
2. Install required software listed above
3. 'bundle install' to install required gems.
4. Adjust the settings in balder.rb or as Heroku config variables (See configuration above)
5. Copy database file (not needed when hosting on Heroku):
	cp config/database.example.yml config/database.yml
6. Create database user and edit database file. (unless on Heroku or using SQLite3)
7. rake db:create
8. rake db:migrate
9. Start up the project with your preferred web-server

### Optional: add photos directly to disk

The gallery has a web-based upload tool. Alternatively you can upload files directly to the upload folder. This means you can import an existing folder based photo collection to Balder.

Put photos in containing folders(albums) in the specified gallery folder.
Hierarchy of folders is not fully supported.

This format is recommended:

- ./ski weekend in hemsedal/snow.jpg
- ./ski weekend in hemsedal/afterski.jpg
- ./trip to iran/beautiful girls in tehran.jpg
- ./trip to iran/mosque in yazd.jpg
- ./trip to iran/powder snow in dizin.jpg

Every time you manually add photos to disk you must scan by visiting /photos/scan or run ScanFiles.Scan(false) from the console.

## Version history

1.4.0
- Ruby 2.3

1.3.0
- Facebook Connect

1.2.3
- Rails 3.2

1.2.2
- Rails 3.1

1.2.1
- Using plupupload instead of uploadify for non-flash upload options. Can now use html5, normal form, silverlight, gears and browserplus for photo upload.

1.2.0
- New storage path: "/uploads/files/" instead of "/uploads/". Make sure you move your photos or adjust the storage path.

## Todo

- Testing... (yeah I know, sorry)

## Ideas

- Themes
- Improved UX
- Mobile/Tablet friendly display using CSS media queries
- Caching

Patches welcome!

## Contributors

Made with help from @formigarafa, @grrowl, @vanicat and @arne.

## Copyright and license info

This code is copyrighted by Espen Antonsen. The source code is available free under the MIT License.
