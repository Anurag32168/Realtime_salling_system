import express from "express"
const app=express();
import cors from "cors"
import mysql from "mysql"

app.use(express.json());
app.use(cors());
const db=mysql.createConnection({
  host:"localhost",
  user:"root",
  password:"a1s1t1i1k1",
  database:"test"
})
//ALTER user 'root'@'localhost' identified with mysql_native_password by 'a1s1t1i1k1';
//ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'a1s1t1i1k1';


app.get("/",(req,res)=>{
  console.log("backend is also open and in running condition")
  res.send("backend is also open and in running condition")
})
app.get("/books",(req,res)=>{
  let q="SELECT * from books";
  db.query(q,(err,data)=>{
    if(err)  return res.json(err);
    return res.json(data);
  })
})
//app.use(express.json());
app.post("/books",(req,res)=>{
  const q="INSERT INTO books(`title`,`desc`,`cover`) VALUES (?)"
  const values=[
    req.body.title,
    req.body.desc,
    req.body.cover
  ]



  db.query(q,[values],(err,data)=>{
    if (err)
      return res.json(err);
      return res.json("Book has been created successfully");
  });
});
app.listen(8800,()=>{
  console.log("server is running on port 8800")
  console.log("connected to backend")
})
# Realtime_salling_system
