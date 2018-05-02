import React, { Component } from 'react';
import { Container, Header, Content, Footer, Text, Title, Body, Left, Right, Form, Item, Label, floatingLabel, Input, Button, H2, H3 } from 'native-base';


class App extends Component {
  constructor(){
    super();
    this.state={massa:'', tinggi: '', IMT:'', category:'', isCalculated:false }
  }


  calculateIMT=() => {
      var x=  this.state.massa/ Math.pow(this.state.tinggi/100, 2)
      var z='BB Anda '
      this.setState({IMT: x})
      if (x < 18.5){
        z+='kurang!'
      }
      else if (x < 25){
        z+='ideal!'
      }
      else if (x < 30){
        z+='berlebih!'
      }
      else if (x < 40){
        z+='sangat berlebih!'
      }
      else {
        z='Anda obesitas!'
      }
      this.setState({category:z, isCalculated:true})
  }

  result(){
    return <Content>
    <Text>Massa Tubuh:</Text>
    <H3>{this.state.massa} kg</H3>
    <Text>Tinggi Badan:</Text>
    <H3>{this.state.tinggi/100} m</H3>
    <Text>Indeks Massa Tubuh:</Text>
    <H3>{this.state.IMT}</H3>
    <Text>Diagnosa:</Text>
    <H3>{this.state.category}</H3>
    </Content>
  }

  render() {

    return (

      <Container >
        <Header>
          <Body>
            <Title>INDEKS MASA TUBUH</Title>
          </Body>
        </Header>
        <Content>
          <Form>
            <Item floatingLabel>
              <Label>Massa (kg)</Label>
              <Input onChangeText={(inputUser) => {this.setState({massa:inputUser, isCalculated:false})}}
               value={this.state.massa} />
            </Item>
            <Item floatingLabel last>
              <Label>Tinggi (cm)</Label>
              <Input onChangeText={(inputUser) => {this.setState({tinggi:inputUser, isCalculated:false})}}
               value={this.state.tinggi}  />
            </Item>
          </Form>
          <Button block onPress={()=>{this.calculateIMT()}}>
            <Text>Hitung IMT</Text>
          </Button>

          { this.state.isCalculated ? this.result() : null }

        </Content>

      </Container>
    );
  }
}


export default App;
