## What is Html?
  HTML or hypertext markup language is a language used to create websites.  
   It consists of a series of elements that determine the structure of the webpage. We begin the file with the <html> tag and end with </html>.  
   The most important rule is that every opening tag has a corresponding closing tag. These only differ by a /.  
   Inside the html tag we have the <head> and <body> tags. The head tag contains all the meta information about the html page. The body tag consists of the elements to be displayed in the page. Heres a starter template for a html file:  
        
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta http-equiv="X-UA-Compatible" content="IE=edge">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Document</title>
        </head>
        <body>

        </body>
        </html>  
    
## Some useful elements:
  Inside the bode tag is where all the elements displayed on the webpage are coded.  

### Header tags:
   Firstly we have the header tag. h1, h2, ..., h5 are used as headers for the document. The greater the number succeding h in the tag the smaller the title gets.  
        
### Text tag:
In order to type a paragraph we use the p tag. Any text can to be displayed can be written in here.  
If the text should be editable by the user then the <textarea> tag generates a box that the user can type in.  
### Image:
 In order to display an image we use the img tag. The source of the image is mapped to the attribute src. The attribute alt is used to display text in case the image fails to load. This text should ideally give a concise description of the image. For example, the below code generates the image found at "https://yourImageURL.com":  
        
      <img src="https://yourImageURL.com" alt="My sample image">
### Video: 
 Similarly in order to insert a video element in the webpage we use the <video> tag. Here we use a seperate <source> tag to provide the link to the video.  
            <video>
                <source src="YourVideo.mp4" type="video/mp4">
            </video>
### Table:
In order to display a table we use the table tag. Inside the table tags we use thead tag for the title row, the tbody tag for all the information rows and the tfoot tag for the concluding row. Inside each of these tags the tr tag is used to start a row and td for the column in it. The th tag is used for the header column inside the tr tags and td inside the <tr> tags in the tfoot section.  
        
            <table>
                <thead>
                    <tr>
                        <th>Column 1</th>
                        <th>Column 2</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>element at row 1 column 1</td>
                        <td>element at row 1 column 2</td>
                    </tr>
                    <tr>
                        <td>element at row 2 column 1</td>
                        <td>element at row 2 column 2</td>
                    </tr>
                </tbody>
                <tfoot>
                    <tr>
                        <td>footer column 1</td>
                        <td>footer column 2</td>
                    </tr>
                </tfoot>
            </table>
The resulting table is: 
    <table>
                <thead>
                    <tr>
                        <th>Column 1</th>
                        <th>Column 2</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>element at row 1 column 1</td>
                        <td>element at row 1 column 2</td>
                    </tr>
                    <tr>
                        <td>element at row 2 column 1</td>
                        <td>element at row 2 column 2</td>
                    </tr>
                </tbody>
                <tfoot>
                    <tr>
                        <td>footer column 1</td>
                        <td>footer column 2</td>
                    </tr>
                </tfoot>
            </table>
### Links:
The a tag is used to provide links to external websites with the href attribute pointing to the desired webpage.  
### Input:
The input tag is used to get information from the user. The type attribute in the tag determines the format of the input. Some types are text, time, date, image and email.  
### Div:
The div tag creates a section in the document. An empty div tag will have size 0. The size of the tag can be manipulated in css or automatically takes the size of the contents in it.
### Lists:
The ul tag is used to create lists. Inside the ul we use li tags for each list element. For example:  
        
            <ul>
                <li> List element 1</li>
                <li> List element 2</li>
            </ul>
## Usage of elements:
Elements can be nested within each other. For example a p may contain text, followed by a table and a list if needed. A p tag could contain another p tag in it as well!  Elemnts will be rendered in the order in which they are coded. 
## Styling:
In order to customise the look of elements html is combined with css to make the webpages look cleaner.
