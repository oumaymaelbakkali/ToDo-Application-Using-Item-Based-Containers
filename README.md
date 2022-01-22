# ToDo-Application-Using-Item-Based-Containers
## Introduction 
The purpose of this Homwork is to create an ToDoApplication for  helping the users to  arrange their tasks,in order to improving thier work and personal life.
## Creating Main Window and Dialog Form
The first step for creating any application is building the interface ,For do this task we will use QT Designer for creating an MainWindow Application  As you see in the image :
![image](https://user-images.githubusercontent.com/93142901/150646573-39d0f671-abf9-4396-813e-8a6714fc634b.png)
Then,we will create Dialog Form for interacting with the user:
![image](https://user-images.githubusercontent.com/93142901/150647261-5e6e4b87-7d53-47c2-9b1d-e7371836480e.png)
## ToDoApplication(Functionality)
 Now we will  write a set of basic functionality :
### New task
Now we will add the function for the New task action:<br/>
first we will Add a public Getter for the line edit Text to get the description task :
 ```cpp
  QString Dialog::Descri() const
  {
      return ui->lineEdit->text();
  }

 ```
  Add a public Getter for the Checkbox to get if the task is finished :
  ```cpp
  bool Dialog::checkbox(){
  if(ui->checkBox->isChecked())
    return 0;
  else
    return 1;
  }

 ```
  Add a public Getter for the ComboBox to get  the Tag of the task :
  ```cpp
  QString Dialog::Combo() {
    return ui->comboBox->currentText();
   }

 ```
  Add a public Getter for the DateEdit to get  the Due date :
  ```cpp
   QString Dialog::Date() const{
    return ui->dateEdit->text();
   }

 ```
 Also we will create an CompareDate() function for compare the Due date that we get with the date of today 
  ```cpp
   bool Dialog::CompareDate(){
    QDate Date=QDate::currentDate();
    if(ui->dateEdit->text()==Date.toString("dd/MM/yyyy")){
        return 0;

    }else
        return 1;
     }

 ```
  Now we will  implement the slot to respond to the action trigger :<br/>
  firstly,we will creating an object D from the class D and if the replay is accepted and the chekbox is no checked and the Due date is ToDay we will add the task in the first      listwidget,else if the the chekbox is no checked and the Due date is not ToDay  we will add the task in planing tasks in listwidget_2,and if the chekbox is checked we will      add the task in finished tasks:
   ```cpp
    void TaskApp::on_actionNewtask_triggered()
    {   
    ui->listWidget->show();
    ui->listWidget_2->show();
    ui->listWidget_3->show();
    Dialog D;
    QDateTime now = QDateTime::currentDateTime();
    auto replay=D.exec();
    if(replay== QDialog::Accepted && D.checkbox()==1 && D.CompareDate()==0){
        QListWidgetItem *item=new QListWidgetItem;
        item->setText(QString( D.Descri()+"  "+D.Combo() +"  " +"Due :"+"  " + D.Date()));
        item->setIcon(QIcon(":/new.png"));
        ui->listWidget->addItem(item);

    }else if(replay==QDialog::Accepted && D.checkbox()==1 && D.CompareDate()==1){
        QListWidgetItem *item2=new QListWidgetItem;
        item2->setText(QString( D.Descri()+"  "+D.Combo() +"  " +"Due :"+"  " + D.Date()+"   tag : 1"));
        item2->setIcon(QIcon(":/task-planning.png"));
        ui->listWidget_2->addItem(item2);

    }else if(replay== QDialog::Accepted && D.checkbox()==0 && D.CompareDate()==1){

        QListWidgetItem *item1=new QListWidgetItem;
        item1->setText(QString( D.Descri()+"  "+D.Combo() +"  " +"Due :"+"  " + D.Date()+"   tag : 0"));
        item1->setIcon(QIcon(":/task-completed.png"));
        ui->listWidget_3->addItem(item1);

    }
    }
  ```
   
  ![image](https://user-images.githubusercontent.com/93142901/150649292-b9193765-a957-420d-84fc-1064c7a9e846.png)
  ![image](https://user-images.githubusercontent.com/93142901/150649547-76c759fe-46fa-4948-88e5-7d529d5b9351.png)
  ![image](https://user-images.githubusercontent.com/93142901/150649621-42fce992-afcf-408d-990c-8d43c8273214.png)



 ### Planing task
  Now we will add the function for the PLannig task action:<br/>
  this action is just for show only planing tasks
  ```cpp
   void TaskApp::on_actiontaskplanning_triggered()
    {  
    ui->listWidget_2->show();
    ui->listWidget->hide() ;
    ui->listWidget_3->hide();

     }

 ```
  ### finished task
  Now we will add the function for the finished task action:<br/>
  this action is just for show only finished tasks
  ```cpp
  void TaskApp::on_actiontaskcompleted_triggered()

   {  ui->listWidget_3->show();
      ui->listWidget->hide() ;
      ui->listWidget_2->hide();

    }

  ```
  ### Delete Action
  We use Delete action  for delete an task selected <br/>
  ```cpp
   void TaskApp::on_actionDelete_triggered()
   {
   QListWidgetItem *it= ui->listWidget->takeItem(mnSelected);
   QListWidgetItem *it1= ui->listWidget_2->takeItem(mnSelected1);
   QListWidgetItem *it2= ui->listWidget_3->takeItem(mnSelected2);
   delete it;
   delete it1;
   delete it2;
   }

    void TaskApp::on_listWidget_currentRowChanged(int currentRow)
   {
    mnSelected = currentRow;
     }

    void TaskApp::on_listWidget_2_currentRowChanged(int currentRow)
     {
      mnSelected1 = currentRow;
      }

      void TaskApp::on_listWidget_3_currentRowChanged(int currentRow)
     {
    mnSelected2 = currentRow;
      }
```
  ### QtAbout Action
  we use this Action for showing a message Box about Qt
  ```cpp
     void TaskApp::on_actionAboutQT_triggered()
    {
    QMessageBox::aboutQt(this,"AboutQT");
    }
  ```
  ### Quit Action
  For quit the application
  ```cpp
     void TaskApp::on_actionquit_triggered()
    {
    this->close();

    }
    
  ```
  
  
  > Excellent job, looking forward to read your second part. Good luck
 
