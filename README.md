
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

Nest is an MIT-licensed open source project. It can grow thanks to the sponsors and support by the amazing backers. If you'd like to join them, please [read more here](https://docs.nestjs.com/support).

## Stay in touch

- Author - [Kamil Myśliwiec](https://twitter.com/kammysliwiec)
- Website - [https://nestjs.com](https://nestjs.com/)
- Twitter - [@nestframework](https://twitter.com/nestframework)

## License

segétlet:
        
        string query = "SELECT * FROM members";
        using (MySqlCommand cmd = new MySqlCommand(query, conn))
        {
            using (MySqlDataReader reader = cmd.ExecuteReader())
            {
                while (reader.Read())
                {
                    long id = Convert.ToInt64(reader["id"]);
                    string name = reader["name"].ToString();
                    string gender;
                    if (reader["gender"] == DBNull.Value)
                        gender = "U";
                    else
                        gender = reader["gender"].ToString();

                    DateTime birthDate = Convert.ToDateTime(reader["birth_date"]);
                    bool banned = Convert.ToBoolean(reader["banned"]);

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


<DataGrid x:Name="MemberGrid" AutoGenerateColumns="False" CanUserAddRows="False" SelectionMode="Single" Width="687">
    <DataGrid.Columns>
        <DataGridTextColumn Header="Név" Binding="{Binding Name}" Width="*"/>
        <DataGridTextColumn Header="Nem" Binding="{Binding Gender}" Width="100"/>
        <DataGridTextColumn Header="Születési dátum" Binding="{Binding BirthDate, StringFormat=yyyy-MM-dd}" Width="150"/>
        <DataGridTextColumn Header="Kitiltva" Binding="{Binding BannedDisplay}" Width="100"/>
    </DataGrid.Columns>
</DataGrid>
