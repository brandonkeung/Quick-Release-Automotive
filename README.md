# Quick-Release-Automotive

Quick Release specializes in providing business services in product data management. They help engineers focus on engineering by improving a company's data quality, allowing for more efficient products. Quick Release has clients from a variety of industries including automotive, aviation, and technology from clients such as Ford, Lucid, Czinger, Joby, and Rivian.

## The Challenge

We’re trying to build an electric vehicle called the “QRV” and we need your help sorting out the data! The engineers have been releasing their parts into the Bill of Materials (BoM) without anyone checking the data quality first. All downstream stakeholders are worried we won’t be able to order the parts we need on time. It’s up to you to find out what’s wrong and report back

## Our Motivation

As data science majors, we are passionate about leveraging data to solve real-world problems such as QRV electric vehicles. Through applying data science skills to optimize a Bill of Materials, we aim to assist in achieving a seamless product development process, ultimately advancing sustainable transportation solutions for the future. In addition, this challenge provides us the opportunity to practice data science preprocessing skills in a realistic problem.

## Exploration and Preprocessing

TODO: 
INCLUDE SOME GRAPHS AND TABLES
Some things we found interesting were... WINDOWS ENCODING!!

- For each given procurement code rule:
   - Find all distinct parents that follow the correct procurement code and sub-component code
   - Find all distinct children that follow the allowed procurement code and sub-component code
   - From the previous list of children, find the number of children that have a parent that follows the parent procurement code and sub-component code.
- From each given procurement code rule, we can add all the number of children that have parents that follow the rules to find the total number of entries that follow the procurement code rules. This results in a  __% error rate.

We have confirmed this percentage through our tree structure as well. By constructing a tree data structure level by level, we were able to add nodes based on whether they can become children of current nodes. We also ruled out nodes or entries that are unable to be added because of the procurement codes. We continued this method until we reached the 12th level (max level) affirming our previous result of a __% error rate.

## Analysis

ML Model

## Challenges

### Understanding the problem

One of the major issues we faced was understanding the task at hand. With a lengthy yet critical introduction, we began to pick apart the objective and found niche rules to follow within our CSV file. We quickly found that some information was not important (distinguishing between tier 1 and tier 2 products) while others were critical in our data cleaning. 


### Runtime 

When constructing our tree data structure, we created many Python scripts and functions to assist in its construction. When attempting to build our tree, we quickly found that the runtime was O(N^3) resulting in wasted hours waiting for our code. Recognizing this limitation, we worked to reduce the runtime to O(N^2) allowing for the construction of our tree to be much faster.

## Future Improvements

To avoid issues in the Bill of Materials, we can Utilize and enforce Database constraints to guarantee that logic errors are avoided. For example, because all parts custom-designed by a company and standard components must have a procurement code, we can enforce that employees editing the Bill of Materials must include a Procurement Code and can not remove Procurement Codes without removing the whole entry. 


## Special Thanks

Thank you to [Data@UCI](https://www.dataatuci.com) and [Quick Release](https://www.quickrelease.co.uk) for hosting the Atlantis 2024 Datathon.

## License

[MIT](https://choosealicense.com/licenses/mit/)