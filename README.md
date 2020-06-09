# scrapyMongoDbExample
This is a Scrapy project to scrape online book store from http://books.toscrape.com/ and store data in mongodb.

This project is only meant for educational purposes.

## Element Selection

Bookstore Website


![Image of Website](https://github.com/Aniruddhsinh03/scrapySeleniumDemo/blob/master/screenshots/bookstore_1.jpg)

Book Url Selection


![Image of BookUrl](https://github.com/Aniruddhsinh03/scrapySeleniumDemo/blob/master/screenshots/bookstore_2.jpg)

Next Page Url Selection


![Image of NextPage](https://github.com/Aniruddhsinh03/scrapySeleniumDemo/blob/master/screenshots/bookstore_3.jpg)


Image Url Selection


![Image of ImageUrl](https://github.com/Aniruddhsinh03/scrapySeleniumDemo/blob/master/screenshots/bookstore_4.jpg)

Title Selection


![Image of Title](https://github.com/Aniruddhsinh03/scrapySeleniumDemo/blob/master/screenshots/bookstore_5.jpg)


Price Selection


![Image of Price](https://github.com/Aniruddhsinh03/scrapySeleniumDemo/blob/master/screenshots/bookstore_6.jpg)

Stock And Ratings Selection


![Image of StockAndRatings](https://github.com/Aniruddhsinh03/scrapySeleniumDemo/blob/master/screenshots/bookstore_7.jpg)

Description Selection


![Image of Description](https://github.com/Aniruddhsinh03/scrapySeleniumDemo/blob/master/screenshots/bookstore_8.jpg)

Product Type,Price Inc Tax,Price Exc Tax,Tax,Availability,Reviews Selection


![Image of ProdtData](https://github.com/Aniruddhsinh03/scrapySeleniumDemo/blob/master/screenshots/bookstore_9.jpg)

Mongodb Stored Data


![Image of MongoDB](https://github.com/Aniruddhsinh03/scrapyMongoDbExample/blob/master/screenshots/mongodb_1.jpg)

## Extracted data

This project extracts availability,description,image_urls,images(download with rename),url,instock_availability,number_of_reviews,price,price__excl_tax,price_incl_tax,product_type,rating,tax,title,upc.
The extracted data looks like this sample:

     {'availability': ['In stock (1 available)'],
      'description': ['England, 1921. Three years after her husband, Alex, '
                 'disappeared, shot down over Germany, Jo Manders still mourns '
                 "his loss. Working as a paid companion to Alex's wealthy, "
                 'condescending aunt, Dottie Forsyth, Jo travels to the '
                 'family’s estate in the Sussex countryside. But there is much '
                 'she never knew about her husband’s origins…and the '
                 'revelation of a mysterious death in the England, 1921. Three '
                 'years after her husband, Alex, disappeared, shot down over '
                 'Germany, Jo Manders still mourns his loss. Working as a paid '
                 "companion to Alex's wealthy, condescending aunt, Dottie "
                 'Forsyth, Jo travels to the family’s estate in the Sussex '
                 'countryside. But there is much she never knew about her '
                 'husband’s origins…and the revelation of a mysterious death '
                 'in the Forsyths’ past is just the beginning…All is not well '
                 "at Wych Elm House. Dottie's husband is distant, and her son "
                 'was grievously injured in the war. Footsteps follow Jo down '
                 'empty halls, and items in her bedroom are eerily rearranged. '
                 'The locals say the family is cursed, and that a ghost in the '
                 'woods has never rested. And when Jo discovers her husband’s '
                 'darkest secrets, she wonders if she ever really knew him. '
                 'Isolated in a place of deception and grief, she must find '
                 'the truth or lose herself forever.And then a familiar '
                 'stranger arrives at Wych Elm House… ...more'],
                 'image_urls': ['http://books.toscrape.com//media/cache/5f/03/5f0345cd81aaad65bb9f6a34ec0f6b9b.jpg'],
                
                 'instock_availability': ['In stock'],
                 'number_of_reviews': ['0'],
                 'price': ['£27.70'],
                 'price__excl_tax': ['£27.70'],
                 'price_incl_tax': ['£27.70'],
                 'product_type': ['Books'],
                 'rating': [' Four'],
                 'tax': ['£0.00'],
                 'title': ['Lost Among the Living'],
                 'upc': ['d510567580c8be52']}

## Configuration

in settings.py set pipeline for download data in mongodb.
command:
        
        TITEM_PIPELINES = {
         'scrapyMongoDbExample.pipelines.ScrapymongodbexamplePipeline': 300,
        }

        MONGODB_SERVER = 'localhost'
        MONGODB_PORT = 27017
        MONGODB_DB = 'books'
        MONGODB_COLLECTION = 'products'
        
        
settings pipelines
            
            lass ScrapymongodbexamplePipeline(object):
    # product details store in database
    # database configuration
    def __init__(self):
        settings = get_project_settings()
        connection = MongoClient(
            settings['MONGODB_SERVER'],
            settings['MONGODB_PORT'])
        db = connection[settings['MONGODB_DB']]
        self.collection = db[settings['MONGODB_COLLECTION']]
    # insert data into database
    def process_item(self, item, spider):
        self.collection.insert(dict(item))
        return item

## Spiders

This project contains one spider and you can list them using the `list`
command:

    $ scrapy list
    scrapySeleniumDataExtractionAndActionDemo

Spider extract the data from book store.




## Running the spiders

You can run a spider using the `scrapy crawl` command, such as:

    $ scrapy crawl scrapySeleniumDataExtractionAndActionDemo

