# Ummul_FrontEnd


Name: - Ummul Zehra
Registration No: - 12017372
College: - Lovely professional University
Assignment Domain: - Frontend Assignment

Question1: - Explain what the simple List component does.
Answer:- The list component in react renders a list of items. A list component takes an array of items as a prop and renders an unordered lists of those items with the option to select a single item from the list. It takes in prop including , the item’s index , whether it is currently selected or not, a function to handle click events, and the text content of the item. The component renders a <li> element with a background colour of green if it is selected and red if it is not, and it calls the click event handler function passed in via props when it is clicked. This component is often used as a child component within a larger list of components where it can be reused multiple times to render each item in the list.
There are several ways to create a list component in React. One of them is ‘map()’ function to loop through an array of items and render a component for each item.
Question 2 :- What problems/ warnings are there with the code?
Answer :- Warning:
Line 31:6: React Hook useEffect has a missing dependency: setSelectedIndex. in variable selectedIndex under WrappedListComponent it must be useState(null) instead of useState()

In SingleListItem component, the isSelected prop type should be PropTypes.bool.isRequired instead of PropTypes.bool. This is because the prop is required, and its value should always be a boolean.

Error:
there is an error in Line 54 under WrappedListComponent.propTypes it shoud be corrected as PropTypes.shape instead of PropTypes.shapeOf as property shapeOf does not exist in type propType.

Question 3 :- Please fix, optimize, and/or modify the components as much as you think is necessary.

Answer :-  Correct code 


import React, { useState, useEffect, memo } from 'react';
import PropTypes from 'prop-types';

// Single List Item
const WrappedSingleListItem = ({
  index,
  isSelected,
  onClickHandler,
  text,
}) => {
  return (
    <li
      style={{ backgroundColor: isSelected ? 'green' : 'red'}}
      onClick={() => onClickHandler(index)}
    >
      {text}
    </li>
  );
};

WrappedSingleListItem.propTypes = {
  index: PropTypes.number,
  isSelected: PropTypes.bool,
  onClickHandler: PropTypes.func.isRequired,
  text: PropTypes.string.isRequired,
};

const SingleListItem = memo(WrappedSingleListItem);

// List Component
const WrappedListComponent = ({
  items,
}) => {
  const [selectedIndex, setSelectedIndex] = useState();

  useEffect(() => {
    setSelectedIndex(null);
  }, [items]);

  const handleClick = index => {
    setSelectedIndex(index);

  };

  return (
    <ul style={{ textAlign: 'left' }}>
      {items ? (
        items.map((item, index) => (
        <SingleListItem
          key={index}
          onClickHandler={() => handleClick(index)}
          text={item.text}
          index={index}
          isSelected={selectedIndex === index}
        />
      ))
            ): (
               <div>Wait...</div>
            )}
    </ul>
  )
};

WrappedListComponent.propTypes = {
  items: PropTypes.arrayOf(PropTypes.shape({
    text: PropTypes.string.isRequired,
  })),
};

WrappedListComponent.defaultProps = {
  items: [
      {text: "Ummul Zehra"},
      {text: "12017372"},
      {text: "B.Tech"},
      {text: "Frontend Assignment"}
  ],
};

const List = memo(WrappedListComponent);

export default List;















