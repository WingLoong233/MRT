# react-mrt

[![NPM](https://img.shields.io/npm/v/react-mrt.svg)](https://www.npmjs.com/package/react-mrt) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

[Demo](https://thudm.github.io/MRT/)

## Introduction

This is the React Component for displaying MRT (Master Reading Tree). The input data can be generated by the python library [mrtframework](https://pypi.org/project/mrtframework/).

If you only want to see the graphical output of your generated MRT, you can directly go to the [demo](https://thudm.github.io/MRT/) page and click the upload button. Once the MRT json file (generated by *mrtframework*) is uploaded, the demo page will display the graphical output of your MRT.

If you want to develop the display of MRT or integrate MRT into your own frontend project, you can use the following instructions to get started.

## Install

```bash
npm install --save react-mrt
```

Notice that the react-mrt depends on several other libraries.

## Usage

```jsx
import React from 'react'
import { MRT, adapters } from 'react-mrt'
import sample_data from './sample.json'
import 'antd/dist/antd.css'
import html2canvas from 'html2canvas'

class App extends React.Component {

  constructor(props) {
    super(props)
    this.state = {
      data: sample_data
    };
  }

  render() {
    const adapter = new adapters.PaperAdapter()
    const adapterInput = {data: this.state.data, userEdits: {}}
    const transformedData = adapter.transform(adapterInput)
    return (
      <div className="App">
        <MRT data={transformedData} authors={["Da Yin", "Weng Lam Tam", "Ming Ding", "Jie Tang"]}
          lang="en" shareable={true} likeable={false} loadable={true} onLoadJson={(json) => this.setState({data: json})}
          html2canvas={html2canvas}/>
      </div>
    );
  }
}

export default App;
```

## Note

When you develop this library, you may encounter a problem associated with "invalid hook call" from React. This is due to the duplicated react instance from two different react library (although they may have the same version). You can link the `react` library in `example` app to the `react-mrt` library by running `npm link example/node_modules/react` to solve this problem.

## License

MIT © [THUDM](https://github.com/thudm)
