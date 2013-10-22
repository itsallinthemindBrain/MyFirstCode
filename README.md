MyFirstCode
===========

/* Vb.net Code for testing GitHub */

Public Class TestTimer
    Private dt As New DataTable
    Private Sub TestTimer_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
        Try
            dt.Columns.Add("ELAPSED TIME")
            RecordTimerDataGridView.DataSource = dt
        Catch ex As Exception
            MsgBox(ex.Message)
        End Try
    End Sub
    Private Sub StartButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles StartButton.Click
        Try
            StopWatchTimer.Start()
            StartButton.Text = "LAP"
        Catch ex As Exception
            MsgBox(ex.Message)
        End Try
    End Sub
    Private Sub StopButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles StopButton.Click
        Dim TimeElapsed As String
        Dim Hour As String = ""
        Dim Minute As String = ""
        Dim Seconds As String = ""
        Try
            If SecondsLabel.Text = 0 Then
                MsgBox("Press Start", MsgBoxStyle.Information)
            Else
                StopWatchTimer.Stop()
                StartButton.Text = "START"
                Hour = HourLabel.Text.ToString
                Minute = MinuteLabel.Text.ToString
                Seconds = SecondsLabel.Text.ToString
                TimeElapsed = Hour & ":" & Minute & ":" & Seconds
                RecordTimeElapsed(TimeElapsed)
            End If
            HourLabel.Text = 0
            MinuteLabel.Text = 0
            SecondsLabel.Text = 0
        Catch ex As Exception
            MsgBox(ex.Message)
        End Try
    End Sub
    Private Sub StopWatchTimer_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles StopWatchTimer.Tick
        Try
            SecondsLabel.Text = SecondsLabel.Text + 1
            If SecondsLabel.Text = 59 Then
                MinuteLabel.Text = MinuteLabel.Text + 1
                SecondsLabel.Text = 0
            End If
            If MinuteLabel.Text = 59 Then
                HourLabel.Text = HourLabel.Text + 1
                MinuteLabel.Text = 0
            End If
        Catch ex As Exception
            MsgBox(ex.Message)
        End Try
    End Sub
    Private Sub RecordTimeElapsed(ByVal TimeElapsed As String)
        Try
            dt.Rows.Add(TimeElapsed)
            MySort()
        Catch ex As Exception
            MsgBox(ex.Message)
        End Try
    End Sub
    Private Sub MySort()
        Dim min, i, j As Integer
        Dim tempName As String
        Try
            For j = 0 To dt.Rows.Count - 1
                min = j
                For i = j + 1 To dt.Rows.Count - 1
                    If StrComp(dt.Rows(i)("Elapsed Time"), dt.Rows(min)("Elapsed Time"), CompareMethod.Text) = -1 Then
                        min = i
                    End If
                    If min <> j Then
                        tempName = dt.Rows(j)("Elapsed Time")
                        dt.Rows(j)("Elapsed Time") = dt.Rows(min)("Elapsed Time")
                        dt.Rows(min)("Elapsed Time") = tempName
                    End If
                Next
            Next
        Catch ex As Exception
            MsgBox(ex.Message)
        End Try
    End Sub
End Class


