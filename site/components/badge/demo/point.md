# 小点

- order: 1

---

````jsx
let Badge = require('uxcore-badge');

class Demo extends React.Component {

    constructor(props) {
        super(props);
        this.state = {
        }
    }

    render() {
        return (
            <Badge dot={true}>
                <a href="#" className="head-example"></a>
            </Badge>
        );
    }
};

ReactDOM.render(
    <Demo />
, document.getElementById('components-badge-demo-point'));
/* JS END CSS START*/
````

````css
.head-example {
    width: 50px;
    height: 50px;
    border-radius: 3px;
    display: inline-block;
    background: #e8e8e8;
}
````
