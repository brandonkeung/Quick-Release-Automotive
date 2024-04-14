# Quick-Release-Automotive

Quick Release specializes in providing business services in product data management. They help engineers focus on engineering by improving a company's data quality, allowing for more efficient products. Quick Release has clients from a variety of industries including automotive, aviation, and technology from clients such as Ford, Lucid, Czinger, Joby, and Rivian.

## The Challenge

We’re trying to build an electric vehicle called the “QRV” and we need your help sorting out the data! The engineers have been releasing their parts into the Bill of Materials (BoM) without anyone checking the data quality first. All downstream stakeholders are worried we won’t be able to order the parts we need on time. It’s up to you to find out what’s wrong and report back

## Our Motivation

As data science majors, we are passionate about leveraging data to solve real-world problems such as QRV electric vehicles. Through applying data science skills to optimize a Bill of Materials, we aim to assist in achieving a seamless product development process, ultimately advancing sustainable transportation solutions for the future. In addition, this challenge provides us the opportunity to practice data science preprocessing skills in a realistic problem.

## Exploration and Preprocessing

![download](https://github.com/brandonkeung/Quick-Release-Automotive/assets/97375525/4a61e89c-069f-4b74-b84a-45f7eb92fe51)
![download](https://github.com/brandonkeung/Quick-Release-Automotive/assets/97375525/8e3d037d-86e2-4967-96ae-4737d3f6038b)
![download](https://github.com/brandonkeung/Quick-Release-Automotive/assets/97375525/a269927e-d4df-4dca-b28f-12efb810961d)

Throughout our exploration, we ran into an issue with downloading and working with the file from a Windows machine. For lines that had no value for Variant, a special character was detected resulting in runtime errors in our Python scripts and SQL queries. Through further investigation, we found that MacOS did not have this issue. To overcome this, on a Windows Machine we used: 

```
quick_release = pd.read_csv("/work/QRV Bill of Materials.csv", encoding='windows-1252')
```

We also noticed many parts were duplicated under the same parent. In short, entire entries were copy and pasted. We determined that these entries were intentional and multiple of the same parts were needed to construct the parent object.

- For each given procurement code rule:
   - Find all distinct parents that follow the correct procurement code and sub-component code
   - Find all distinct children that follow the allowed procurement code and sub-component code
   - From the previous list of children, find the number of children that have a parent that follows the parent procurement code and sub-component code.
- From each given procurement code rule, we can add all the number of children that have parents that follow the rules to find the total number of entries that follow the procurement code rules. This results in a 15.47% error rate.

We have a similar percentage through our tree structure as well. By constructing a tree data structure level by level, we were able to add nodes based on whether they can become children of current nodes. We also ruled out nodes or entries that are unable to be added because of the procurement codes. We continued this method until we reached the 12th level (max level) achieving a 23% error rate. ~ 53K nodes correct

## Analysis
![download](https://github.com/brandonkeung/Quick-Release-Automotive/assets/97375525/a474f8a3-cb3a-408b-914b-ae3a5acf7ccd)

In order to find out more about our data, we used a RandomForestClassifcation model to accurately predict whether an entry was valid. Our model had an accuracy score of 95.32%. However, more importantly, we ran feature importance on our model and determined that Procurement Code Make was the most impactful feature by far. When evaluating what part of the QRV vehicle is impacted the most, we determine the battery pack is also very influential compared to its counterparts. With a negative correlation between System_Battery Pack and IS VALID, we determine that when an entry is related to the Battery Pack, it is more likely to be invalid. In addition, we observed a negative correlation between Joey Tribbiani and IS VALID, determining that the manager may need to help Joey with entering parts into the BoM.

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
