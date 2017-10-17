import renderer from 'react-test-renderer';
import React, { Component } from 'react';
import { shallow, mount, render } from 'enzyme';
import {App, tick, parseURL} from '../src/App.js';

describe('Just work', () => {
    it('render should work', () => {
        const wrapper = shallow( <App />)
        expect(wrapper).toMatchSnapshot();
        // TODO : more to come
    })
    it('tick should work', () => {
        expect(tick(11)).not.toEqual(undefined)
        expect(tick(10)).toEqual({minutes: '00', seconds: '10'})
        expect(tick(61)).toEqual({minutes: '01', seconds: '01'})
        expect(tick(120)).toEqual({minutes: '02', seconds: '00'})
    }) 
    it('tick should handle negative numbers', () => {
        expect(tick(-10)).toEqual({minutes: '00', seconds: '00'})
    })
    it('should handle empty arguments', () => {
        expect(tick()).toEqual({minutes: '00', seconds: '00'})   
    })
    it('should only handle a integer as argument', () => {
        expect(tick('hejsan')).toEqual({minutes: '00', seconds: '00'})     
    })
})

describe('Parse url', () => {
    const url = 'https://mapage.com?sec=123&min=2&anything=something'
    it('should parse url', () => {
        const p = parseURL(url) 
        expect(p['sec']).toEqual('123')
        expect(p['min']).toEqual('2')
        expect(p['anything']).toEqual('something')
    })
    it('should handle empty url', () => {
        expect(parseURL('')).toEqual({})
    })
    it('should handle incorrect url', () => {
        expect(parseURL(12309123)).toEqual({})
        expect(parseURL('hehehe123')).toEqual({})
        expect(parseURL('hejan12309123')).toEqual({})
        expect(parseURL([])).toEqual({})
        expect(parseURL({})).toEqual({})   
        expect(parseURL(2 + 2)).toEqual({})
        expect(parseURL(true)).toEqual({})
        expect(parseURL(NaN)).toEqual({})
        expect(parseURL(undefined)).toEqual({})
    })
    it('should handle empty parameter', () => {
        const u = 'https://mapage.com?='
        expect(parseURL(u)).toEqual({"": ""})
    })
})
