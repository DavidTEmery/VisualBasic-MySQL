' David Emery 12/08/14
' A Visual Basic app that represents a MySQL table in ListBox

Imports MySql.Data.MySqlClient

Public Class Form1
    Dim cn As New MySqlConnection
    Dim querystring As String
    Dim cmd As MySqlCommand
    Dim DR As MySqlDataReader

    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        Try
            ' This string is for development purposes. DO NOT use root user id in production!
            cn.ConnectionString = "server=localhost;user id=root;database=test"
            cn.Open()
            'MsgBox("Connected!")

            ' A Label on the form for displaying connection status:
            lblStatus.ForeColor = Color.Green
            lblStatus.Text = "Connected!"

            'this string holds the MySQL query for selecting all(*) from the event table
            querystring = "select * from users"
            ' A command is created with the query and the connection string
            cmd = New MySqlCommand(querystring, cn)
            DR = cmd.ExecuteReader

            While DR.Read
                'adds to list:
                lbEvents.Items.Add(DR.Item("username"))
            End While

        Catch connectionError As System.ArgumentException
            'MsgBox("Connection Failed")
            lblStatus.ForeColor = Color.Red
            lblStatus.Text = "Connection Failed"
        Catch MySQLError As MySql.Data.MySqlClient.MySqlException
            lblStatus.ForeColor = Color.Red
            lblStatus.Text = "Connection Failed"

        End Try

    End Sub


    Private Sub ListBox1_SelectedIndexChanged(sender As Object, e As EventArgs) Handles lbEvents.SelectedIndexChanged

    End Sub

    Private Sub Label1_Click(sender As Object, e As EventArgs) Handles lblStatus.Click
        MsgBox(lblStatus.Text)
    End Sub

End Class
