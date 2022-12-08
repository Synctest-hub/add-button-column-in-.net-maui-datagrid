# add-button-column-in-.net-maui-datagrid

The .NET MAUI [DataGrid](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataGrid.SfDataGrid.html)(SfDataGrid) allows to load any template views in the [DataGridTemplateColumn](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataGrid.DataGridTemplateColumn.html). In this article, you can learn about how to load the button for specific column and perform any action on the button click.

## C#
Create the ButtonCommand with execute method to delete current row when performing click action on the button.

```C#
    public class ViewModel : INotifyPropertyChanged
    {
        private ObservableCollection<OrderInfo> orderInfo;
        private ICommand buttonCommand;
        public ObservableCollection<OrderInfo> OrderInfoCollection
        {
            get { return orderInfo; }
            set { this.orderInfo = value; RaisePropertyChanged("OrderInfoCollection"); }
        }

        public ICommand ButtonCommand
        {
            get { return buttonCommand; }
            set { buttonCommand = value; }
        }

        public ViewModel()
        {
            this.OrderInfoCollection = new ObservableCollection<OrderInfo>();
            this.GenerateOrders();
            this.ButtonCommand = new Command(DeleteRecord);
        }

        public void GenerateOrders()
        {
            orderInfo.Add(new OrderInfo(1001, "Ana Trujillo", "Mexico", "ANATR"));
            orderInfo.Add(new OrderInfo(1002, "Ant Fuller", "Mexico", "ANTON"));
            orderInfo.Add(new OrderInfo(1003, "Thomas Hardy", "UK", "AROUT"));
            orderInfo.Add(new OrderInfo(1004, "Tim Adams", "Sweden", "BERGS"));
            orderInfo.Add(new OrderInfo(1005, "Hanna Moos", "Germany", "BLAUS"));
            orderInfo.Add(new OrderInfo(1006, "Andrew Fuller", "France", "BLONP"));
            orderInfo.Add(new OrderInfo(1007, "Martin King", "Spain", "BOLID"));
            orderInfo.Add(new OrderInfo(1008, "Lenny Lin", "France", "BONAP"));
            orderInfo.Add(new OrderInfo(1009, "John Carter", "Canada", "BOTTM"));
            orderInfo.Add(new OrderInfo(1010, "Laura King", "UK", "AROUT"));
            orderInfo.Add(new OrderInfo(1011, "Ant Fuller", "Mexico", "ANTON"));
            orderInfo.Add(new OrderInfo(1012, "Thomas Hardy", "UK", "AROUT"));
            orderInfo.Add(new OrderInfo(1013, "Tim Adams", "Sweden", "BERGS"));
            orderInfo.Add(new OrderInfo(1014, "Hanna Moos", "Germany", "BLAUS"));
            orderInfo.Add(new OrderInfo(1015, "Andrew Fuller", "France", "BLONP"));
            orderInfo.Add(new OrderInfo(1016, "Martin King", "Spain", "BOLID"));
            orderInfo.Add(new OrderInfo(1017, "Lenny Lin", "France", "BONAP"));
            orderInfo.Add(new OrderInfo(1018, "John Carter", "Canada", "BOTTM"));
            orderInfo.Add(new OrderInfo(1019, "Laura King", "UK", "AROUT"));
        }

        private void DeleteRecord(object orderInfo)
        {
            this.OrderInfoCollection.Remove(orderInfo as OrderInfo);
        }

        #region INotifyPropertyChanged

        public event PropertyChangedEventHandler PropertyChanged;

        private void RaisePropertyChanged(string name)
        {
            if (PropertyChanged != null)
                this.PropertyChanged(this, new PropertyChangedEventArgs(name));
        }

        #endregion
    }

```

## XAML
Create a DataGridTemplateColumn with button inside and bind a command property of the button to the ButtonCommand property of ViewModel.

```XAML
<syncfusion:SfDataGrid x:Name="dataGrid" AutoGenerateColumnsMode="None" ItemsSource="{Binding OrderInfoCollection}" DefaultColumnWidth="130" GridLinesVisibility="Both" HeaderGridLinesVisibility="Both">
        <syncfusion:SfDataGrid.Columns>
            <syncfusion:DataGridNumericColumn MappingName="OrderID" HeaderText="ID"></syncfusion:DataGridNumericColumn>
            <syncfusion:DataGridTextColumn MappingName="Customer" HeaderText="Name"></syncfusion:DataGridTextColumn>
            <syncfusion:DataGridTextColumn MappingName="Country"></syncfusion:DataGridTextColumn>
            <syncfusion:DataGridTemplateColumn MappingName="CustomerID">
                <syncfusion:DataGridTemplateColumn.CellTemplate>
                    <DataTemplate>
                        <Button Text="Delete" Command="{Binding Source={x:Reference dataGrid},Path=BindingContext.ButtonCommand}"  CommandParameter="{Binding .}"></Button>
                    </DataTemplate>
                </syncfusion:DataGridTemplateColumn.CellTemplate>
            </syncfusion:DataGridTemplateColumn>
        </syncfusion:SfDataGrid.Columns>
    </syncfusion:SfDataGrid>
```
