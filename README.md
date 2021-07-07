# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)




<input placeholder="enter here" onChange={setToken}></input>
const [token,settoken] = useState();
  const setToken = (e)=>{
    settoken(e.target.value);
  }

  ae9cb87fd0c069c65b23f867c67d923febbe5f41df24a2f98cf87fd5745a7d23

  const post= ()=>{
    fetch(`https://gitlab.com/api/v4/users/9180082/projects?access_token=${token}`)
        .then(response => response.json())
        .then(res => {
          data=res;
          console.log(data);
        });
  }
   const fetchPosts = async () => {
      setLoading(true);
      const res = await axios.get('https://gitlab.com/api/v4/users?username=rithikagarwal2');
     
      console.log(res);
      setuserid(res.data[0].id);
      console.log(res.data[0].id);
      const projects= await axios.get(`https://gitlab.com/api/v4/users/${res.data[0].id}/projects?access_token=a47babe4ca273839ce99dc4e4a568ec343a17b3ca830128699c32b0f4e1c5555`);

      console.log(projects);
      var arr =[];
      projects.data.map((obj)=>{
        arr.push(obj.id);
      })
      setPosts(arr);
      setLoading(false);
      console.log(arr);
    };

    fetchPosts();

    <table>
  <tr>
    <th>Project Id</th>
    <th>Project Name</th>
    <th>Pipeline Status</th>
   
  </tr>
  {props.pid.map((element)=>{
         return (<tr>
           <td>{element[0]}</td>
           <td>{element[1]} </td>
           <td> --- </td>
         </tr>);
     })}

  
</table>
<Table
      columns={["Name", "Age", "Address"]}
      data={[
        [
          "Sarah Brown",
          31,
          "100 Broadway St., New York City, New York"
        ],
        [
          "Jane Smith",
          32,
          "100 Market St., San Francisco, California"
        ]
      ]}
    />


     
      
      <Pagination
        postsPerPage={props.postsPerPage}
        totalPosts={props.totalPosts}
        paginate={props.paginate}
      />






       useEffect(()=>{
  const fetchProjectids = async () => {
    
    const userdata= await axios.get('https://gitlab.com/api/v4/user?access_token=a47babe4ca273839ce99dc4e4a568ec343a17b3ca830128699c32b0f4e1c5555');
    //console.log(userdata);
    const username= userdata.data.username;
    //console.log(username);
    const res = await axios.get(`https://gitlab.com/api/v4/users?username=${username}`);
   
    //console.log(res);
    
    //console.log(res.data[0].id);

    const projects= await axios.get(`https://gitlab.com/api/v4/users/${res.data[0].id}/projects`);
    console.log(projects);
    //console.log(projects);
    let arr =[];
    arr.push([36528,"Bitcoin"]);
    projects.data.map((obj)=>{
      arr.push([obj.id,obj.name]);
      //console.log(arr);
    })
    let array_to_pass=[];
    arr.forEach(async (element)=>{
        const merge_ids_response= await axios.get(`https://gitlab.com/api/v4/projects/${element[0]}/merge_requests`);

        //console.log(merge_ids_response);
        if(merge_ids_response.data.length===0){
          array_to_pass.push([element[1],null,null,null,null]);
          console.log("entered");
        }
        else{
          merge_ids_response.data.forEach(async (merge_req)=>{
                    
                      if(merge_req.iid!==null){
                      const Pipeline_status = await axios.get(`https://gitlab.com/api/v4/projects/${element[0]}/merge_requests/${merge_req.iid}/pipelines`);
                      //console.log(Pipeline_status);
                            if(Pipeline_status.data.length==0){
                      array_to_pass.push([element[1],merge_req.title,(merge_req.merged_by===null?null:merge_req.merged_by.name),null,null]);
                            }
                            else{
                              let Pipeline_stat= Pipeline_status.data[0].status;
                              let Approval;
                              if(Pipeline_stat=="success"){
                                Approval= "Approved";
                              }
                              else{
                                Approval= "Not_Approved_Yet";
                              }

                       array_to_pass.push([element[1],merge_req.title,(merge_req.merged_by===null?null:merge_req.merged_by.name),Approval,Pipeline_status]);
                            }
                      }
                      else{
                        array_to_pass.push([element[1],merge_req.title,(merge_req.merged_by===null?null:merge_req.merged_by.name),null,null]);
                      }
                   


                  
               

          })
        }

    });


  settuple(array_to_pass);
    
    //console.log(array_to_pass);
    
  };

  fetchProjectids();
},[]);