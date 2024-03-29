import './App.css'
import React from 'react';
import ParamEditor from './ParamEditor';

interface p{
  id:number,
  name:string,
  type:string,
}
const params:p = [
  {
    id: 1,
    name: 'Назначение',
    type: 'string',
  },
  {
    id: 2,
    name: 'Длина',
    type: 'string',
  },
];

interface m{
paramId:number,
value:string,
paramValues:any,

}
const model = {
  paramValues: [
    {
      paramId: 1,
      value: 'повседневное',
    },
    {
      paramId: 2,
      value: 'макси',
    },
  ],
};

const App: React.FC = () => {
  return (
    <div>
      <ParamEditor params:p={params} model:m={model} />
    </div>
  );
};

export default App;



















import React, { Component } from 'react';

interface Param {
  id: number;
  name: string;
  type: 'string';
}

interface ParamValue {
  paramId: number;
  value: string;
}
interface Color{
  
}
interface Model {
  paramValues: ParamValue[];
  colors: Color[];
}

interface Props {
  params: Param[];
  model: Model;
}

interface State {
  paramValues: ParamValue[];
}
class ParamEditor extends Component<Props, State> {
    constructor(props: Props) {
      super(props);
      this.state = {
        paramValues: props.model.paramValues,
      };
    }
  
    handleParamChange = (paramId: number, value: string) => {
      this.setState((prevState) => ({
        paramValues: prevState.paramValues.map((param) =>
          param.paramId === paramId ? { ...param, value } : param
        ),
      }));
    };
  
    getModel = (): Model => {
      return {
        paramValues: this.state.paramValues,
        colors: this.props.model.colors,
      };
    };
  
    render() {
      return (
        <div>
          <h2>Param Editor</h2>
          {this.props.params.map((param) => (
            <div key={param.id}>
              <label>{param.name}</label>
              <input
                type="text"
                value={
                  this.state.paramValues.find((pv) => pv.paramId === param.id)?.value || ''
                }
                onChange={(e) => this.handleParamChange(param.id, e.target.value)}
              />
            </div>
          ))}
        </div>
      );
    }
  }
  
  export default ParamEditor;
