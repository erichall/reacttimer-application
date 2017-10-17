import React, { Component } from 'react';
import './style.css';

// Copyright (c) 2010-2013 Diego Perini, MIT licensed
// https://gist.github.com/dperini/729294
function validateURL(value) {
    return /^(?:(?:(?:https?|ftp):)?\/\/)(?:\S+(?::\S*)?@)?(?:(?!(?:10|127)(?:\.\d{1,3}){3})(?!(?:169\.254|192\.168)(?:\.\d{1,3}){2})(?!172\.(?:1[6-9]|2\d|3[0-1])(?:\.\d{1,3}){2})(?:[1-9]\d?|1\d\d|2[01]\d|22[0-3])(?:\.(?:1?\d{1,2}|2[0-4]\d|25[0-5])){2}(?:\.(?:[1-9]\d?|1\d\d|2[0-4]\d|25[0-4]))|(?:(?:[a-z\u00a1-\uffff0-9]-*)*[a-z\u00a1-\uffff0-9]+)(?:\.(?:[a-z\u00a1-\uffff0-9]-*)*[a-z\u00a1-\uffff0-9]+)*(?:\.(?:[a-z\u00a1-\uffff]{2,})).?)(?::\d{2,5})?(?:[/?#]\S*)?$/i.test( value ) || /http:\/\/\d{3}.\d{3}.\d.\d{3}:\d{4}/;
}

export function parseURL(url) {
    if(!validateURL(url))
        return {}
    var params = {};
    const search = decodeURIComponent(url.slice(url.indexOf('?') + 1));
    const defs = search.split('&');

    defs.forEach((val,key) => {
        const parts = val.split( '=', 2);
        params[ parts[0]] = parts[1];
    });
    return params; 
}

export function tick(timer) {
    if(timer < 0 || timer === undefined || isNaN(timer))
        return {minutes: '00', seconds: '00'}

    var minutes = parseInt(timer / 60, 10);
    var seconds = parseInt(timer % 60, 10);
    return {
        minutes: minutes < 10 ? "0" + minutes : minutes.toString(),
        seconds: seconds < 10 ? "0" + seconds : seconds.toString(),
    };
}

export class App extends Component {

    constructor (props) {
        super(props);

        this.state = {
            minutes: '00',
            seconds: '00',
        };
    }

    componentDidMount() {
        const params = parseURL(window.location.href);
        const sec = this.setCustomConfig(params);
        this.startTimer(sec);
    }
    setCustomConfig(params) {
        const keys = Object.keys(params)
        if(keys.length === 1) {
            const s = Object.keys(params)[0];
            return !isNaN(s) ? parseInt(s,10) : 180 
        }
        // TODO: add more config features
        return 180;
    }

    startTimer(duration) {
        var timer = duration;
        setInterval(() => {
            var time = tick(timer);
            this.setState({
                minutes: time.minutes,
                seconds: time.seconds,
            });
            if(--timer < 0)
                timer = duration;
        }, 1000);
    }

    render() {
        return (
            <div className='outer'>
                <div className='middle'>
                    <h1 className='timer'>  {this.state.minutes + ':' + this.state.seconds} </h1>
                </div>
            </div>
        );
    }
}

