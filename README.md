
## Description

[Nest](https://github.com/nestjs/nest) framework TypeScript starter repository.
Linkek:
https://summer-tempo-907.notion.site/Useful-Links-1d4a9da79c3680c48230d0db7a25b568
Useful Links
https://summer-tempo-907.notion.site/Useful-Links-1d4a9da79c3680c48230d0db7a25b568

Java GUI
http://faragocsaba.hu/java-stdlibs-gui

MySql
https://dev.mysql.com/doc/connector-net/en/connector-net-tutorials-sql-command.html

HGabor git
https://github.com/hgabor

dokumentum: (https://github.com/user-attachments/files/20540169/Szoftverfejleszto_mintavizsga1_2023-Automatikusan-mentett1.docx)


Parancsok:
Frontend:
- npx create-react-app bookclubfrontend
  cd bookclubfrontend
  
- npm install bootstrap( // src/index.js import 'bootstrap/dist/css/bootstrap.min.css';)

Backend:
- npm i -g @nestjs/cli
  nest new bookclubbackend
  
- cd bookclubbackend
  npm install @nestjs/typeorm typeorm mysql2

- nest generate module members
  nest generate service members
  nest generate controller members

- nest generate module payments
  nest generate service payments
  nest generate controller payments




## Project setup

```bash
$ npm install
```

## Compile and run the project

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Run tests

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## Resources

Check out a few resources that may come in handy when working with NestJS:

- Visit the [NestJS Documentation](https://docs.nestjs.com) to learn more about the framework.
- For questions and support, please visit our [Discord channel](https://discord.gg/G7Qnnhy).
- To dive deeper and get more hands-on experience, check out our official video [courses](https://courses.nestjs.com/).
- Visualize your application graph and interact with the NestJS application in real-time using [NestJS Devtools](https://devtools.nestjs.com).
- Need help with your project (part-time to full-time)? Check out our official [enterprise support](https://enterprise.nestjs.com).
- To stay in the loop and get updates, follow us on [X](https://x.com/nestframework) and [LinkedIn](https://linkedin.com/company/nestjs).
- Looking for a job, or have a job to offer? Check out our official [Jobs board](https://jobs.nestjs.com).

## Support

- Author - [Kamil Myśliwiec](https://twitter.com/kammysliwiec)
- Website - [https://nestjs.com](https://nestjs.com/)

segétlet:
       public List<Member> members = new List<Member>();

public Statisztika()
{
    LoadMembers();
}
private void LoadMembers()
{
    try
    {
        string connStr = "server=localhost;user=root;database=vizsga-konyvklub;port=3306";
        using (MySqlConnection conn = new MySqlConnection(connStr))
        {
            conn.Open();
            string query = "SELECT * FROM members";
            using (MySqlCommand cmd = new MySqlCommand(query, conn))
            {
                using (MySqlDataReader reader = cmd.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        long id = reader.GetInt64("id");
                        string name = reader.GetString("name");
                        int gender = reader.IsDBNull("gender") ? "Ismeretlen" : reader.GetString("gender");
                        DateTime birthDate = reader.GetDateTime("birth_date");
                        bool banned = reader.GetBoolean("banned");
                        members.Add(new Member(id, name, gender, birthDate, banned));
                    }
                }
            }
        }
    }
    catch (Exception ex)
    {
        Console.WriteLine("Hiba az adatbázis elérésekor: " + ex.Message);
        Environment.Exit(1);
    }
}
public void Futtatas()
{
    KitiltottakSzama();
    VanE18EvAlatti();
    LegidosebbTag();
    NemekSzerint();
    KeresesNevAlapjan();
}

private void KitiltottakSzama()
{
    int count = Members.FindAll(m => m.Banned).Count;
    Console.WriteLine($"Kitiltott tagok száma: {count}");
}
-------

<DataGrid x:Name="MemberGrid" AutoGenerateColumns="False" CanUserAddRows="False" SelectionMode="Single" Width="687">
    <DataGrid.Columns>
        <DataGridTextColumn Header="Név" Binding="{Binding Name}" Width="*"/>
        <DataGridTextColumn Header="Nem" Binding="{Binding Gender}" Width="100"/>
        <DataGridTextColumn Header="Születési dátum" Binding="{Binding BirthDate, StringFormat=yyyy-MM-dd}" Width="150"/>
        <DataGridTextColumn Header="Kitiltva" Binding="{Binding BannedDisplay}" Width="100"/>
    </DataGrid.Columns>
</DataGrid>

----------
app:

import React, {useEffect, useState} from 'react';
import './App.css';
import MemberList from './components/MemberList';
import AddMemberFrom from'./components/AddMemberFrom';

function App() {
  const[members, setMember] = useState([]);
  const [successMessage, setsuccesMessage] = useState('');

  const loadMembers = async () => {
    try{
      const response = await fetch('/api/members');
      const data = await response.json();
      setMember(data); 
    }catch (error){
      console.error("Hiba a tagok lekérdezésekor :" , error);
    }
  };

  useEffect(() => {
    loadMembers();
  }, []);
  return (
    <div className='container py4'>
      <header className='mb-4'>
        <h1>Petrik kövnyklub</h1>
        <nav className='nay'>
          <a className='nav-link' href='#add-member'>Új tag felvétele</a>
          <a className='nav-link' href='https://petrik.hu/' target='_blank' rel='noreferrer'>Petrik honlap</a>
        </nav>
      </header>
      {successMessage && (
        <div className='alert alert-success'>{successMessage}</div>
      )}
      <MemberList members={members} onPaySuccess={() => {
        setsuccesMessage("Sikeres befizetés!");
        setTimeout(() => setsuccesMessage(""), 3000);
      }}/>
      <section id='add-member' className='mt-5'>
        <AddMemberFrom onMemberAdded={loadMembers}/>
      </section>
      <footer className='text-center mt-5'>
        <small>Készítette: Schweitzer Ádám</small>
      </footer>
    </div>
  );
}

components (Card):

import React from "react";

const MemberCard = ({ member, onPaySuccess }) => {
  const getImageForGender = (gender) => {
    switch (gender) {
      case 'Férfi':
        return '/images/male.png';
      case 'Nő':
        return '/images/female.png';
      default:
        return '/images/other.png';
    }
  };

  const handlePayment = async () => {
    try {
      const response = await fetch(`/api/members/${member.id}/pay`, {
        method: 'POST',
      });
      if (!response.ok) {
        const errorData = await response.json();
        alert(errorData.message || 'Hiba történt a befizetés során.');
      } else {
        onPaySuccess();
      }
    } catch (error) {
      alert('Hálózati hiba a befizetés során.');
    }
  };

  return (
    <div className="card mb-4 shadow-sm">
      <div className="card-body text-center">
        <h5 className="card-title">{member.name}</h5>
        <img
          src={getImageForGender(member.gender)}
          alt="Neme"
          style={{ width: '60px', height: '60px' }}
          className="my-2"
        />
        <p>Születési dátum: {member.birthDate}</p>
        <p>Csatlakozás ideje: {member.joinDate}</p>
        <button className="btn btn-success mt-2" onClick={handlePayment}>
          Tagdíj befizetés
        </button>
      </div>
    </div>
  );
};

export default MemberCard;
