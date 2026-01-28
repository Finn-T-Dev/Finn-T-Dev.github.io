---
title: 'UI Prototype with Noesis'
description: 'Developing a UI prototype using NoesisGUI Middleware'
image:
    url: '/images/NoesisProject/noesis-logo-blue.svg'
    alt: 'GitHub wallpaper'
platform: Unreal Engine 5
stack: Noesis Studio, NoesisGUI
---

Experimenting with the Noesis middleware for creating User Interfaces for video games. Exploring functionality through implementing menu navigation and in-game HUD elements.

<img class="pro-img" src="/images/MainMenu_Hierarchy.png" alt="UI layout overview">

The UI layout shows the different components and how they interact with each other. This modular approach makes it easier to maintain and update individual elements.

<img class="pro-img" src="/images/UI_Layout_Noesis.png" alt="UI layout overview">

The hierarchy structure demonstrates how the menu system is organised, with nested components that can be easily modified without affecting other parts of the interface.

I approached this by first building the main menu elements, using grids to position individual elements.
The first challenge was binding the functionality of the buttons to UE5 blueprint logic using commands in NoesisStudio. By binding the button's click action to a named action matching a UE5 Noesis View blueprint function, i was able to implement logic for the start game button to open the main level, and the other buttons opened their respective menus. 

First data binding challenge: The codex.

I wanted my Noesis view to read from my game logic (the model) using the data context (view model). To accomplish this, I created a blueprint data structure to house the shape of incoming data.

```xaml
<Page
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
  mc:Ignorable="d"
  d:DesignWidth="1920"
  d:DesignHeight="1080"
  Background="#FF4D5052">
  
  <Page.Resources>
    <ResourceDictionary>
      <ResourceDictionary.MergedDictionaries>
        <ResourceDictionary Source="GlobalResources.xaml"/>
      </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
  </Page.Resources>
  
  <Grid x:Name="Master">
    <Grid x:Name="Background">
      <Grid.Background>
        <ImageBrush ImageSource="Assets/scifi_main_menu.jpg" Stretch="UniformToFill"/>
      </Grid.Background>
      <Grid x:Name="HeaderBar" Background="#FF000000" Height="32" VerticalAlignment="Top"/>
      <Grid x:Name="FooterBar" Height="32" Background="#FF000000" VerticalAlignment="Bottom"/>
    </Grid>
    <Grid x:Name="Interface">
      <Grid.RowDefinitions>
        <RowDefinition Height="64"/>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="51*"/>
        <RowDefinition Height="838*"/>
        <RowDefinition Height="64"/>
      </Grid.RowDefinitions>
      <Grid.ColumnDefinitions>
        <ColumnDefinition Width="64"/>
        <ColumnDefinition Width="1*"/>
        <ColumnDefinition Width="1*"/>
        <ColumnDefinition Width="1*"/>
        <ColumnDefinition Width="64"/>
      </Grid.ColumnDefinitions>
      <Grid x:Name="TitleArea" Grid.Row="1" Grid.Column="2" Margin="0">
        <TextBlock x:Name="TitleText" Text="Generic Shooter Template" TextWrapping="Wrap" HorizontalAlignment="Center" FontFamily="Broadway" FontSize="56"/>
      </Grid>
      <Grid x:Name="SubtitleArea" Grid.Row="2" Grid.Column="2" HorizontalAlignment="Center" Margin="0,12,0,12">
        <TextBlock x:Name="SubtitleText" Text="You&apos;ve seen it all before" TextWrapping="Wrap" FontSize="24"/>
      </Grid>
      <StackPanel x:Name="MenuStack" Grid.Row="3" Grid.Column="2" Grid.RowSpan="2">
        <Button x:Name="StartButton" Content="START" Command="{Binding StartCommand}" Style="{StaticResource SciFiButtonStyle}"/>
        <Button x:Name="CodexButton" Content="CODEX" Command="{Binding CodexCommand}" Style="{StaticResource SciFiButtonStyle}"/>
        <Button x:Name="SettingsButton" Content="SETTINGS" Command="{Binding SettingsCommand}" Style="{StaticResource SciFiButtonStyle}"/>
        <Button x:Name="ExitButton" Content="EXIT" Command="{Binding ExitCommand}" Style="{StaticResource SciFiButtonStyle}"/>
      </StackPanel>
    </Grid>
  </Grid>
</Page>
```xaml

