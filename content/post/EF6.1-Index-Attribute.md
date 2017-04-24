+++
date = "2013-03-23T11:40:41+01:00"
title = "Index Attribute in EF 6.1"
tags = ["Entity Framework", "EF6.1", ".NET"]
menu = ""
 banner = "banners/entity-framework.png"
+++

Early last week Entity Framework 6.1 [went RTM](http://blogs.msdn.com/b/adonet/archive/2014/03/17/ef6-1-0-rtm-available.aspx).

Amongst the usual performance improvements and a bunch of other stuff that will probably come in useful was the addition of [Index Attributes](http://msdn.microsoft.com/en-US/data/jj591583#Index), which allow the developer to create indexes by annotating their code first models.

This attribute allows the creation of unique indexes as well as supporting multi-column indexes.

A project I'm working on at the moment has the following entity



    public class Pledge
    {
	    public int Id {get;set;}
        public int AttendeeId {get;set;}
        public int ProjectId {get;set;}
        public int EventId {get;set;}
    
        //other properties
    }



A Pledge must be unique to an Attendee, an Event and a Project

Prior to EF 6.1, there was no way to annotate your properties and have EF create the database with the indexes already set up. You would have had to create your database then write a migration specfically for the index, like this.




	public partial class AddUniqueIndexToPledge : DbMigration
    {
        public override void Up()
        {
            CreateIndex("dbo.Pledge",new[]{"AttendeeId","ProjectId", "EventId"},true);
        }
         
        public override void Down()
        {
            DropIndex("dbo.Pledge", new[]{"AttendeeId","ProjectId", "EventId"});
        }
    }


Not so difficult, but it's still an extra step rather than just creating the database with the indexes already added.

Now with Entity Framework 6.1 we can do the below


    public class Pledge
    {
        public int Id {get;set;}
        [Index("IX_AttendeeEventProjectIndex", IsUnique = true, IsClustered = false)
        public int AttendeeId {get;set;}
        [Index("IX_AttendeeEventProjectIndex", IsUnique = true, IsClustered = false)
        public int ProjectId {get;set;}
        [Index("IX_AttendeeEventProjectIndex", IsUnique = true, IsClustered = false)
        public int EventId {get;set;}
        
        
    }



Which will create the following index



    CREATE UNIQUE NONCLUSTERED INDEX [IX_AttendeeEventProjectIndex] ON [dbo].[Pledges]
    (
    [AttendeeId] ASC,
    [EventId] ASC,
    [ProjectId] ASC
    )WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, IGNORE_DUP_KEY = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
    GO



  